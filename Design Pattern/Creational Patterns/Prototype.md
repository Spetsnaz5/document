```
Prototype（原型模式） 是一種創建型設計模式，允許你通過複製現有的物件來創建新物件，而不是通過 new 關鍵字
來創建新的實例。這樣可以節省創建物件的開銷，尤其是當物件初始化成本高昂時非常有用。

優點：
    提高效能：
        通過複製來創建物件，比使用 new 關鍵字創建新物件效率更高，尤其當物件的初始化成本較高時。
    簡化物件創建邏輯：
        使用 Prototype 模式可以減少創建過程中的配置或初始化代碼。
    避免耦合：
        可以動態複製物件而不需要依賴具體類別，降低類別之間的耦合。
缺點：
    深層複製的實現較為複雜：
        當物件含有複雜的引用型態屬性（如嵌套物件、陣列）時，需要額外的深層複製邏輯。
    可能違反單一職責原則：
        __clone() 方法的實現可能會變得過於複雜，從而使得 Prototype 類別不僅負責物件的行為，還負責複製邏輯。

實際應用情境
    原型範本系統：
        如果系統中某個類別的實例化過程非常耗時（如文件解析、數據庫查詢），可以使用原型模式來提前創建一個範本，
        之後通過 clone 來生成新物件。
    遊戲開發中角色物件的複製：
        當創建新角色時，可以基於範本角色來進行複製，然後調整屬性（如名稱、屬性值），而不需要每次都從頭
```

```php
<?php

// 1. 定義 Prototype 接口（或抽象類別）
abstract class BookPrototype {
    protected $title;
    protected $author;

    // 設定書名
    public function setTitle($title) {
        $this->title = $title;
    }

    // 取得書名
    public function getTitle() {
        return $this->title;
    }

    // 強制實現 clone 方法
    abstract public function __clone();
}

// 2. 具體 Prototype 實現類別
class ScienceBookPrototype extends BookPrototype {
    // 設定此類型書的屬性（這裡只是舉例）
    protected $category = "Science";

    // 實現 clone 方法
    public function __clone() {
        // 可根據需要進行深層複製或初始化
        echo "Cloning a science book: {$this->title}\n";
    }
}

class HistoryBookPrototype extends BookPrototype {
    protected $category = "History";

    public function __clone() {
        echo "Cloning a history book: {$this->title}\n";
    }
}

// 3. 使用 Prototype 模式來創建對象
$scienceBookPrototype = new ScienceBookPrototype();
$historyBookPrototype = new HistoryBookPrototype();

// 設置原型書的屬性
$scienceBookPrototype->setTitle("A Brief History of Time");
$historyBookPrototype->setTitle("The History of the Ancient World");

// 通過 clone 來創建新書籍
$book1 = clone $scienceBookPrototype;
$book2 = clone $historyBookPrototype;

// 自訂新書名
$book1->setTitle("The Universe in a Nutshell");
$book2->setTitle("Guns, Germs, and Steel");

// 測試輸出
echo $book1->getTitle() . "\n";  // The Universe in a Nutshell
echo $book2->getTitle() . "\n";  // Guns, Germs, and Steel

```
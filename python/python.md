* 命名規則
    
     module_name,
     package_name,
     ClassName,
     method_name,
     ExceptionName,
     function_name,
     GLOBAL_CONSTANT_NAME,
     global_var_name,
     instance_var_name,
     function_parameter_name,
     local_var_name.


- 避免使用的命名法

    1. 除了計數器及迭代器之外，不要用單一字母為變數命名。
    2. package 及 module 的名稱中不要包含破折號 "-"
    3. 變數名稱前後不要加上兩個雙底線 (如：__double_leading_and_trailing_underscore__ )。

- 命名慣例

    1. "internal" 指 module 內或 class 中的 private 或 protected 的變數。
    2. 要保護 module 變數或函式，可在變數名稱前加上單一底線，若用 from foo import * 時，這些變數不會被 import。
    (編案：若用 from foo import _var 則還是能使用 _var 變數)。
    若要在 class 內宣告 private 變數或方法，則在變數名或 方法名之前加上兩個底線 (__)，private 的效果是透過 name mangling 達成。
    (編案： name mangling 本質上只是把變數重新命名，因此使用者若執意要呼叫 private 變數還 是能夠達成。)
    3. 把相關的 class 及 頂層的 function 放在同一個 module 中。你不需要像 Java 般 限制每個 module 只能有一個 class。
    4. 命名 class 時，使用每個單字的字首用單寫 (如：CapWords)。
    命名 module 時，用 小寫及底線 (如：lower_with_under.py)。
    雖然某些既有的 module 命名仍使用大寫字母(如：CapWords.py)，但不建議這麼做，因為當 module 名稱與 class 名稱相同時它 們將難以分辨。
    (你通常寫 import StringIO 或 from StringIO import StringIO ?)

- 命名通則

    package: lower_with_under (public)
    
    modules: lower_with_under (public), _lower_with_under (internal)
    
    classes: CapWords (public) _CapWords (internal)
    
    exceptions: CapWords (public)
    
    functions: lower_with_under() (public), _lower_with_under() (internal)
    
    global/class constants: CAPS_WITH_UNDER (public), _CAPS_WITH_UNDER (private)
    
    global/class variables: lower_with_under (public), _lower_with_under (private)
    
    instance variables: lower_with_under (public), _lower_with_under (protected), __lower_with_under (private)
    
    method names: lower_with_under() (public), _lower_with_under() (protected), __lower_with_under() (private)
    
    function/method parameters: lower_with_under
    
    local variables: lower_with_under (public)

* Main

即使是一個 script，也應該要能被 import，import 別人後的 script 也不該有副作用。

主函式要放在 main() 函式中。在 Python 中, pychecker, pytdoc, 及 unit test 的 module 都應該能被 import。

為確保 module 被 import 時不會執行主程式，每一個 module 在執行主程式前都應先檢查 if __name__ == '__main__'。

    def main():
        ...
    
    if __name__ == '__main__':
        main()
    
當一個 module 被 import 時，頂層的所有程式碼都會被執行。

因此，在頂層不應該有呼 叫函式、創建物件、或執行不該在使用 pycheck 或 pydoc 時被執行的動作。

編後語
------

保持一致 在編修程式時，花幾分鐘看一看整體的程式碼以得知其風格。

若所有的運算符旁都有空格 ，你也要空格。若原本的註解旁有用井字圈起來的方格，你的註解也應該加上井字方格。

風格指南的重點在於讓寫程式設計師在寫程式時擁有共通的字彙，所以在編寫的過程後能 專注在要寫什麼，而非如何去寫。

我們告訴各位整體的風格規則來讓各位瞭解這些字彙。

然而，個別的風格也是重要的。

若你在一個檔案中加入了一段風格截然不同的程式片段， 讀者們的節奏會被打亂。

避免這種事發生。

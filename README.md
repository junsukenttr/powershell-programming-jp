# PowerShell プログラミング
*このドキュメントは、README.mdの練習として記述しています。嘘はありません。*

PowerShell2.0からは、「モジュール」と呼ばれる機能があります。
モジュールは、目的別に、1つのフォルダの中に作成します。
* 自作したスクリプト(.ps1, .psm1)
* 設定ファイル(.psd1, .ps1xml)
* ヘルプファイル(*-Help.xml)
* データベースのライブラリなどのDLL(.DLL)
* 国際化データ(*.psd1)  各言語ごとに表示するメッセージを変更したりします*

モジュールを作成できるように、PowerShell プログラミングを進めます。

## １．スクリプトブロック
*[about_Script_Blocks](http://technet.microsoft.com/ja-jp/library/dd315277.aspx) microsoft online help.*

*PS > man about_Script_Blocks*

### スクリプトブロックを作る

PowerShellプログラミングの最小単位は、スクリプトブロックです。

スクリプトブロックを記述しただけでは実行されません。

``` PowerShell
    PS > # 文字列を返すscriptblock
    PS > # [scriptblock]型のオブジェクトが生成され、ToString()の結果が表示されている。
    PS > # 実行されていない。
    PS > {"the script block code"}
    "the script block code"
    
    PS > # 計算結果を返すscriptblock
    PS > {$a + $b - $c * $d / $e}
    $a + $b - $c * $d / $e
    
    PS > # [scriptblock]は、System.Management.Automation.ScriptBlockのアクセラレーター
    PS > # Create(string) スタティックメソッドで、スクリプトブロックを生成します
    PS > [scriptblock]::Create("`$a + `$b - `$c * `$d / `$e")
    $a + $b - $c * $d / $e
```

実行するには、呼び出し演算子(&)を直前につけます。

``` PowerShell
    PS > & {"the script block code"}
    the script block code
    
    PS > $a=$b=$c=$d=$e=1
    PS > & {$a + $b - $c * $d / $e}
    1
    
    PS > # scriptblockを変数に格納します。
    PS > $scriptblock = [scriptblock]::Create("`$a + `$b - `$c * `$d / `$e")
    PS > 
    PS > $a=$b=$c=$d=$e=1
    PS > & $scriptblock
    1
    PS > $a=1; $b=2; $c=3; $d=4; $e=5
    PS > & $scriptblock
    0.6
```

### スクリプトブロックで引数を取る

スクリプトブロックで引数を定義して実行します。

``` PowerShell
    PS > # str1とstr2を引数にします。
    PS > {param($str1, $str2) "$str1 is $str2 definition"}
    param($str1, $str2)
    "$str1 is $str2 definition"
    
    PS > # &を前につけて、引数を後ろにつけて実行します。
    PS > & {param($str1, $str2) "$str1 is $str2 definition"} param argument
    param is argument definition
    
    PS > # 引数の型を定義して実行します。
    PS > & {param([int]$num1, [int]$num2) $num1 + $num2} 1 2
    3
    
    PS > # $_
    PS > & {param([int]$num1, [int]$num2) $num1 + $num2} 1 2
```

## ２．関数
## ３．高度な関数
## ４．フィルター
## ５．永続化：スクリプトファイル(.ps1)
## ６．高度な永続化：モジュール(.psd1, .psm1, .ps1xml)

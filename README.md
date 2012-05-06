# PowerShell プログラミング

## １．スクリプトブロック
*[about_Script_Blocks](http://technet.microsoft.com/ja-jp/library/dd315277.aspx) microsoft online help.*

*PS > man about_Script_Blocks*

### スクリプトブロックを作る

PowerShellプログラミングの最小単位は、スクリプトブロックです。

スクリプトブロックを記述しただけでは実行されません。

``` perl
    PS > # 文字列を返すscriptblock
    PS > # [scriptblock]型のオブジェクトが生成され、ToString()の結果が表示されている。
    PS > # 実行されていない。
    PS > {"the script block code"}
    PS > "the script block code"
    
    PS > # 計算結果を返すscriptblock
    PS > {$a + $b - $c * $d / $e}
    PS > $a + $b - $c * $d / $e
    
    PS > # [scriptblock]は、System.Management.Automation.ScriptBlockのアクセラレーター
    PS > # Create(string) スタティックメソッドで、スクリプトブロックを生成します
    PS > [scriptblock]::Create("`$a + `$b - `$c * `$d / `$e")
    PS > $a + $b - $c * $d / $e
```

実行するには、&:呼び出し演算子を直前につけます。

``` perl
    PS > & {"the script block code"}
    PS > the script block code
    
    PS > $a=$b=$c=$d=$e=1
    PS > & {$a + $b - $c * $d / $e}
    PS > 1
    
    PS > # scriptblockを変数に格納します。
    PS > $scriptblock = [scriptblock]::Create("`$a + `$b - `$c * `$d / `$e")
    PS > 
    PS > $a=$b=$c=$d=$e=1
    PS > & $scriptblock
    PS > 1
    PS > $a=1; $b=2; $c=3; $d=4; $e=5
    PS > & $scriptblock
    PS > 0.6
```

### スクリプトブロックで引数を取る

## ２．関数
## ３．高度な関数
## ４．フィルター
## ５．永続化：スクリプトファイル(.ps1)
## ６．高度な永続化：モジュール(.psd1, .psm1, .psxml)

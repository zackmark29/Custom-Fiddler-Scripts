- Copy and paste this to: "C:\Users\ADMIN\Documents\Fiddler2\Scripts\CustomRules.js"

```js
static function Decompressed(output: String): String {
    return output.Replace("-i --raw -o 0.dat", "-L -vvv --compressed");
}

BindUIButton("Copy HAR")
ContextAction("Copy HAR")
public static function CopyAsHar(arrSess: Session[])
{
    var oExportOptions = FiddlerObject.createDictionary();

    oExportOptions.Add("ExportToString", "true");
    oExportOptions.Add("MaxBinaryBodyLength", 1000000);
    oExportOptions.Add("MaxTextBodyLength", 1000000);

    FiddlerApplication.DoExport("HTTPArchive v1.2", arrSess, oExportOptions, null);
    var output = Decompressed(oExportOptions["OutputAsString"]);
    Utilities.CopyToClipboard(output);
    FiddlerApplication.UI.SetStatusText("Copied Sessions as HAR");
}

BindUIButton("Copy cURL")
ContextAction("Copy cURL")
public static function CopyAsCurl(arrSess: Session[])
{
    var oExportOptions = FiddlerObject.createDictionary();

    oExportOptions.Add("ExportToString", "true");

    FiddlerApplication.DoExport("cURL Script", arrSess, oExportOptions, null);
    var output = Decompressed(oExportOptions["OutputAsString"]);
    Utilities.CopyToClipboard(output);
    FiddlerApplication.UI.SetStatusText("Copied Sessions as cURL");
}
```

## REFERENCES
 - https://textslashplain.com/2015/12/30/whats-new-in-fiddler-4-6-2/ 
 - https://feedback.telerik.com/fiddler/1361405-add-copy-as-curl-to-the-list-of-right-click-options
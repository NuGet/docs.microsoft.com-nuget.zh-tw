1. 變更為包含 `.nupkg` 檔案的資料夾。

1. 執行下列命令，指定套件名稱並使用您的 API 金鑰來取代金鑰值：

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. dotnet 會顯示發行程序的結果：

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

請參閱 [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)。
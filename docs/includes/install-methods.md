有三種安裝套件的方法：

| 方法 | 說明 | 參考資料 |
| --- | --- | --- |
| nuget.exe CLI：`nuget install <package_name>` | 下載 \<package_name\> 所識別的套件，並在目前目錄的資料夾中展開其內容。 如未指定任何套件，請安裝專案的 `packages.config` 檔案中列出的所有套件。 不對任何專案檔進行任何變更。 亦請下載並展開相依性。 | [CLI 參考](../tools/nuget-exe-CLI-Reference.md) |
| 套件管理員主控台 (Visual Studio)：`Install-Package <package_name>` | 下載套件並將其安裝到目前的專案，然後更新專案檔，將套件列出為相依性。 | [套件管理員主控台指南](../tools/Package-Manager-Console.md) |
| 套件管理員 UI (Visual Studio) | 提供 UI，透過該 UI 可瀏覽、選取及安裝套件至專案。 更新專案檔，將套件列出為相依性。 | [套件管理員 UI 參考](../tools/Package-Manager-UI.md) |
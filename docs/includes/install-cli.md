#### <a name="windows"></a>Windows
1. 請瀏覽[nuget.org/downloads](https://nuget.org/downloads)選取 3.3 或更高版本的 NuGet （2.8.6 與不相容單聲道）。 一律建議的最新版本，而且 4.1.0+，才能發行至 nuget.org 的封裝。
2. 每個下載`nuget.exe`直接檔案。 指示瀏覽器，以將檔案儲存到您選擇的資料夾。 檔案是*不*的安裝程式; 如果您直接從瀏覽器執行您不會看到任何項目。
3. 新增您放置資料夾`nuget.exe`您從任何地方使用 CLI 工具的 PATH 環境變數。

#### <a name="macoslinux"></a>macOS/Linux
由作業系統發佈行為可能會稍微不同。

1. 安裝[Mono 4.4.2 或更新版本](http://www.mono-project.com/docs/getting-started/install/)。
2. 執行下列命令殼層提示字元：
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. 下列指令碼至適當的檔案加入您的作業系統來建立別名 (通常`~/.bash_aliases`或`~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. 重新載入殼層。  輸入測試安裝`nuget`不含任何參數。 NuGet CLI 說明應該會顯示。
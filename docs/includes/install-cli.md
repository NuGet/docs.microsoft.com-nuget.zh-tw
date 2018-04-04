#### <a name="windows"></a><span data-ttu-id="197a0-101">Windows</span><span class="sxs-lookup"><span data-stu-id="197a0-101">Windows</span></span>
1. <span data-ttu-id="197a0-102">請瀏覽[nuget.org/downloads](https://nuget.org/downloads)選取 3.3 或更高版本的 NuGet （2.8.6 與不相容單聲道）。</span><span class="sxs-lookup"><span data-stu-id="197a0-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="197a0-103">一律建議的最新版本，而且 4.1.0+，才能發行至 nuget.org 的封裝。</span><span class="sxs-lookup"><span data-stu-id="197a0-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
2. <span data-ttu-id="197a0-104">每個下載`nuget.exe`直接檔案。</span><span class="sxs-lookup"><span data-stu-id="197a0-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="197a0-105">指示瀏覽器，以將檔案儲存到您選擇的資料夾。</span><span class="sxs-lookup"><span data-stu-id="197a0-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="197a0-106">檔案是*不*的安裝程式; 如果您直接從瀏覽器執行您不會看到任何項目。</span><span class="sxs-lookup"><span data-stu-id="197a0-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
3. <span data-ttu-id="197a0-107">新增您放置資料夾`nuget.exe`您從任何地方使用 CLI 工具的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="197a0-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="197a0-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="197a0-108">macOS/Linux</span></span>
<span data-ttu-id="197a0-109">由作業系統發佈行為可能會稍微不同。</span><span class="sxs-lookup"><span data-stu-id="197a0-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="197a0-110">安裝[Mono 4.4.2 或更新版本](http://www.mono-project.com/docs/getting-started/install/)。</span><span class="sxs-lookup"><span data-stu-id="197a0-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>
2. <span data-ttu-id="197a0-111">執行下列命令殼層提示字元：</span><span class="sxs-lookup"><span data-stu-id="197a0-111">Execute the following commands at a shell prompt:</span></span>
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. <span data-ttu-id="197a0-112">下列指令碼至適當的檔案加入您的作業系統來建立別名 (通常`~/.bash_aliases`或`~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="197a0-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. <span data-ttu-id="197a0-113">重新載入殼層。</span><span class="sxs-lookup"><span data-stu-id="197a0-113">Reload the shell.</span></span>  <span data-ttu-id="197a0-114">輸入測試安裝`nuget`不含任何參數。</span><span class="sxs-lookup"><span data-stu-id="197a0-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="197a0-115">NuGet CLI 說明應該會顯示。</span><span class="sxs-lookup"><span data-stu-id="197a0-115">NuGet CLI help should display.</span></span>
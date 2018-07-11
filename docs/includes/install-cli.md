#### <a name="windows"></a><span data-ttu-id="cc5d3-101">Windows</span><span class="sxs-lookup"><span data-stu-id="cc5d3-101">Windows</span></span>

1. <span data-ttu-id="cc5d3-102">請瀏覽 [nuget.org/downloads](https://nuget.org/downloads) 並選取 NuGet 3.3 或更高版本 (2.8.6 與 Mono 不相容)。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="cc5d3-103">一律建議使用最新版本，需要 4.1.0 以上版本才能將套件發行至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="cc5d3-104">每個下載項目直接是 `nuget.exe` 檔案。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="cc5d3-105">指示您的瀏覽器將檔案儲存到您選擇的資料夾。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="cc5d3-106">該檔案*不是*安裝程式；如果直接從瀏覽器執行，您將不會看到任何項目。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="cc5d3-107">將放置 `nuget.exe` 的資料夾新增至您的 PATH 環境變數中，以便從任何地方使用 CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="cc5d3-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="cc5d3-108">macOS/Linux</span></span>

<span data-ttu-id="cc5d3-109">行為可能會隨作業系統發佈而稍微不同。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="cc5d3-110">安裝 [Mono 4.4.2 或更新版本](http://www.mono-project.com/docs/getting-started/install/)。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="cc5d3-111">在殼層提示字元中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="cc5d3-111">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="cc5d3-112">將下列指令碼加入到適用於您的作業系統的檔案 (通常為 `~/.bash_aliases` 或 `~/.bash_profile`) 來建立別名：</span><span class="sxs-lookup"><span data-stu-id="cc5d3-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="cc5d3-113">重新載入殼層。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-113">Reload the shell.</span></span>  <span data-ttu-id="cc5d3-114">輸入 `nuget` (不含任何參數) 來測試安裝。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="cc5d3-115">NuGet CLI 說明應該會顯示。</span><span class="sxs-lookup"><span data-stu-id="cc5d3-115">NuGet CLI help should display.</span></span>

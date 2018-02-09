<span data-ttu-id="c3531-101">從您在 nuget.org 上的設定檔，選取 [管理套件] 以查看您剛發行的套件。</span><span class="sxs-lookup"><span data-stu-id="c3531-101">From your profile on nuget.org, select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="c3531-102">您也會收到確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="c3531-102">You also receive a confirmation email.</span></span> <span data-ttu-id="c3531-103">請注意，可能需要一些時間才會編製套件的索引，並顯示在其他人可以找到它的搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="c3531-103">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="c3531-104">在這段期間，套件頁面會顯示下列訊息：</span><span class="sxs-lookup"><span data-stu-id="c3531-104">During that time your package page shows the message below:</span></span>

    ![This package has not been indexed yet. It will appear in search results and will be available for install/restore after indexing is complete.](../media/QS_Create-03-NotIndexed.png)

<span data-ttu-id="c3531-105">就是這麼容易！</span><span class="sxs-lookup"><span data-stu-id="c3531-105">And that's it!</span></span> <span data-ttu-id="c3531-106">您剛剛已將第一個 NuGet 套件發行至 nuget.org，其他開發人員可以在他們自己的專案中使用它。</span><span class="sxs-lookup"><span data-stu-id="c3531-106">You've just published your first NuGet package to nuget.org that other developers can use in their own projects.</span></span>

<span data-ttu-id="c3531-107">如果您在本逐步解說中建立的套件不是真的很實用 (例如，使用空類別庫建立的套件)，則您應該「取消列出」該套件，以便在搜尋結果中加以隱藏：</span><span class="sxs-lookup"><span data-stu-id="c3531-107">If in this walkthrough you created a package that isn't actually useful (such as a package created with an empty class library), you should *unlist* the package to hide it from search results:</span></span>

1. <span data-ttu-id="c3531-108">在 nuget.org，選取您的使用者名稱 (頁面右上方)，然後選取 [管理套件]。</span><span class="sxs-lookup"><span data-stu-id="c3531-108">On nuget.org, select your user name (upper right of the page), then select **Manage Packages**.</span></span>

1. <span data-ttu-id="c3531-109">在 [已發行] 下方找出您想要取消列出的套件，然後選取右邊的資源回收筒圖示：</span><span class="sxs-lookup"><span data-stu-id="c3531-109">Locate the package you want to unlist under **Published** and select the trash can icon on the right:</span></span>

    ![針對 nuget.org 上列出之套件顯示的資源回收筒圖示](../media/qs_create-vs-03-trash-can.png)

1. <span data-ttu-id="c3531-111">在後續頁面上，清除標籤為 [在搜尋結果中列出 (package-name)] 的方塊，然後選取 [儲存]：</span><span class="sxs-lookup"><span data-stu-id="c3531-111">On the subsequent page, clear the box labeled **List (package-name) in search results** and select **Save**:</span></span>

    ![針對 nuget.org 上的套件清除 [列出] 核取方塊](../media/qs_create-vs-04-unlist.png)
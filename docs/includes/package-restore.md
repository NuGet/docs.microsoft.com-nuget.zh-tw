- **套件管理員 UI** (Visual Studio)：以滑鼠右鍵按一下方案總管中的解決方案，然後選取 [還原 NuGet 套件]。 如有一或多個個別套件仍未正確安裝 (表示方案總管顯示錯誤圖示)，請使用套件管理員 UI 解除安裝受影響的套件，再重新安裝。 請參閱[重新安裝和更新套件](../Consume-Packages/Reinstalling-and-Updating-Packages.md)

- **命令列**：使用 [nuget restore](../tools/cli-ref-restore.md) 命令。 只要在專案資料夾中執行 `nuget restore` 就會嘗試還原專案的相依性。

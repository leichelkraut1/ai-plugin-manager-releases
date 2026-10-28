# AI Plugin Manager

Manage plugins from multiple GitHub stores in **Codex**, **Claude Code**, or both, on Windows and Apple Silicon Mac. Choose what to install, enable, disable, and remove. Adding a store never installs its plugins automatically.

## Download and install

Get the latest beta from [Releases](https://github.com/leichelkraut1/ai-plugin-manager-releases/releases). App downloads and updates are public and need no GitHub account. The app includes its .NET runtime.

Third-party license and attribution notices are included in `THIRD-PARTY-NOTICES.txt` beside the application files.

- **Windows x64:** download `win-x64-setup.exe` and run the per-user installer. It adds a Start menu shortcut and needs no administrator rights. A portable ZIP is also available; portable copies use manual app updates.
- **Apple Silicon Mac:** download `osx-arm64.dmg`, open it, and copy **AI Plugin Manager.app** into Applications. A ZIP is also available. Run the installed copy, rather than the copy inside the disk image, to use app updates.

Mac beta builds are ad-hoc signed and are **not Apple Developer ID signed or notarized**. macOS may block the first launch. If you choose to run the beta, allow only the exact app downloaded from this release page through **System Settings → Privacy & Security**. Do not disable Gatekeeper globally. Windows and Intel Mac upgrade tests run in CI; Apple Silicon execution still needs a user pilot.

Install the Codex and/or Claude Code clients you want to manage, and Git. Private plugin stores use [GitHub CLI](https://cli.github.com/) for browser sign-in and credential storage. App updates do not require GitHub CLI. Missing client tools are reported in the app.

## Browse stores and choose plugins

1. Choose **Add store**. Enter a GitHub marketplace repository URL or choose **Load from file…** to read a shared store connection JSON.
2. Choose a label, Work/Personal group, and tracked branch, tag, or commit. For private stores, sign in and select a GitHub account with access. For public stores, choose **Public repository (no account)**.
3. Review the catalog and each plugin's included components. A plugin can contain skills, tools, hooks, agents, and other executable components; its components install together.
4. Select one plugin or check several. Choose **Codex**, **Claude Code**, or both, then **Install**, **Enable**, **Disable**, or **Uninstall**.

**Disable** keeps a plugin installed but turns it off. **Enable** turns it on again. **Uninstall** removes its installation from the selected client. Installing an existing disabled plugin leaves it disabled until you enable it explicitly.

Bulk actions report results for each plugin and client. A failure does not undo successful actions. Cancel stops the remaining work; refresh client status if a command was interrupted.

Removing a store subscription leaves its native plugin installations in place. Uninstall them first if you also want those removed. Work/Personal labels organize stores; they do not isolate accounts, projects, or AI conversations.

## See everything installed

The **All installed** view shows plugins reported by your local Codex and Claude Code clients, including plugins installed outside this manager. Search or filter by client, then enable, disable, or uninstall one or several selected installations.

These actions need no store subscription or GitHub sign-in. **Store not added** means the manager has no matching store subscription. **Refresh client status** rereads native state.

Only user-level installations can be changed here. Project, local, organization-managed, and ambiguous entries are read-only. Manage them in the owning client or project. Loose skill folders and other profiles are separate.

## VS Code and other environments

Installing for Codex or Claude Code also covers its local VS Code extension when it uses the same user profile. There is no separate VS Code destination. Start a fresh AI session after changes.

The manager operates on local client installations. WSL, remote SSH hosts, containers, cloud sessions, Claude chat, and Cowork have separate installations or management. Organization policies can still restrict changes.

## Updates are your choice

**Plugin updates:** opt in separately for each store to check at most once daily while the manager is open, or choose **Update installed** manually. Existing disabled plugins stay disabled, and new catalog entries stay uninstalled. Codex updates installed plugins at marketplace scope; Claude Code supports individual plugin updates.

**App updates:** open **App updates** and choose **Check for updates**. No account or sign-in is needed. **Check for app updates automatically** starts off; enable it and **Save preferences** for daily checks while the app is open. **Include beta releases** starts on because current releases are betas.

When an app release is available, review it and choose **Update and restart**. The manager verifies the download, installs the update, and reopens. Automatic checks never install or restart by themselves. Your stores, preferences, and native plugins are preserved.

- Windows updates use the existing per-user installer.
- Mac updates replace a writable installed app bundle. The previous bundle is retained for recovery if the replacement fails to confirm startup. Apps running from a disk image, a translocated path, or a location you cannot write require manual installation first.
- Portable and development copies use manual downloads.

Closing the app stops its checks; native client updaters are separate. Users upgrading from **0.4.0 or earlier** should install a current release once to switch to public app updates without repository access.

## Share a store connection

Ask the store owner for a connection JSON, or create one with this format:

```json
{
  "schema": 1,
  "displayName": "Team tools",
  "group": "Work",
  "repositoryUrl": "https://github.com/your-org/your-marketplace",
  "ref": "stable"
}
```

Use **Add store → Load from file…**, review the fields, and choose **Read catalog and add store**. Loading a file does not install plugins or turn on updates. Each user selects their own account for private stores. Keep credentials, account names, and plugin selections out of connection files.

Private store connections and plugin contents are not bundled with the app. Getting the manager does not grant access to a private store.

## Privacy and troubleshooting

Store choices and update preferences are saved locally. GitHub CLI manages private-store credentials through operating-system facilities; tokens are not saved in the manager's state. GitHub authorization is separate from signing into your AI clients.

- **Private store not found:** sign in and select an account with access. Also check the repository URL and tracked ref.
- **Client missing on Mac:** Finder can use a different PATH from Terminal. Install the client in a standard location and reopen the manager.
- **Read-only installation:** manage it through its project, organization, or owning client.
- **App update needs attention:** read the result in **App updates**. You can always download the current installer from the release page.

Uninstalling the manager leaves native plugins and saved store choices in place. Use the manager's uninstall actions first if you want plugins removed as well.

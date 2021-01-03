# macOS Big Sur Post Install Changes

- Install macOS Big Sur
 - Sign in with Apple ID
 - Enable Location Services
 - Enable Touch ID
 - Enable Siri

- Users & Groups
 - Set User Photo

- Trackpad
 - Tap to click (On)

- Accessibility
 - Pointer Control -> Trackpad Options… -> Enable dragging (three finger)
 - Zoom -> Use scroll gesture with modifier keys to zoom: ^ Control

- Safari Preferences
 - Search -> DuckDuckGo
 - AutoFill -> Uncheck All

- Dock & Menu Bar Preferences
 - Minimise windows into application icon (On)
 - Minimise windows using Scale effect (On)
 - Automatically hide and show the Dock (On)
 - Spotlight -> Show in Menu Bar (Off)
 - Siri -> Show in Menu Bar (Off)
 - Show recent applications in Dock (Off)

- TextEdit Preferences
 - Format -> Plain Text

- Security & Privacy
 - Use your Apple Watch to unlock apps and your Mac (On)
 - Firewall (On)

- Spotlight
 - Remove all categories
 - Check
  - Applications
  - System Preferences

- Desktop & Screen Saver
 - Desktop
  - Big Sur (Dynamic)
 - Screen Saver
  - Ken Burns -> Big Sur
  - Hot Corners
   - Bottom Right -> Start Screen Saver

- Display
 - Resolution -> Scaled (Alt) -> 2560 x 1440

- Font
 - https://www.jetbrains.com/lp/mono/#how-to-install

- Finder
 - Sidebar
  - Home Drive (On)
  - iCloud Drive (Off)
  - Recent Tags (Off)
  - Dragged Home Drive to top

- Homebrew Package Manager
 - /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
 - Installs Command Line Tools for Xcode

- git (2.29.2)
 - brew install git
  - zsh completions and functions have been installed to: /usr/local/share/zsh/site-functions

- Docker (3.0.3,51017)
 - brew install --cask docker

- Visual Studio Code (1.52.1)
 - brew install --cask visual-studio-code
 - Extensions
  - Remote - Containers
 - Icons
  - VSCode Icons
 - Appearance
  - Move Sidebar to Right
 - Settings
  - Font Family - 'JetBrains Mono', Menlo, Monaco, 'Courier New', monospace

- Visual Studio 2019 for Mac (8.8.4.30)
 - brew install --cask visual-studio

- GitHub CLI (1.4.0)
 - brew install gh

- Authy (1.8.3)
 - brew install --cask authy

- 1Password (7.7)
 - brew install --cask 1password
 - Enable extension in Safari

- Spotify (1.1.48.625.g1c87c7f7,1.1.48.625.g1c87c7f7-60)
 - brew install --cask spotify

- Logitech Options (8.36.76)
 - https://download01.logi.com/web/ftp/pub/techsupport/options/Options_8.36.76.zip
 - Granted Logi Options & Logi Options Daemon Accessibility privileges in Security & Privacy
 - Granted Logi Options Daemon Input Monitoring Privileges in Security & Privacy

- Parallels (16.1.2-49151)
 - brew install --cask parallels
 - Granted access to Desktop, Documents and Downloads folders
 - Installed Windows 10 image
 - Granted access to Camera & Microphone
 - Signed in and activated license
 - Granted Parallels Desktop Accessibility privileges in Security & Privacy
 - Preferences
  - Virtual Machine Dock Icons - None

- Git GPG Commit Signing
 - https://medium.com/better-programming/how-to-sign-your-git-commits-1014edaf1e85
 - sudo chown -R $(whoami) /usr/local/share/man/man8
 - chmod u+w /usr/local/share/man/man8
 - brew install gpg
 - brew install pinentry-mac
 - Added 'pinentry-program /usr/local/bin/pinentry-mac' to ~/.gnupg/gpg-agent.conf
 - Added 'use-agent' to ~/.gnupg/gpg.conf
 - Added 'export GPG_TTY=$(tty); gpgconf --launch gpg-agent' to ~/.zshrc
  - Sourced ~/.zshrc
 - Ran 'gpg --full-gen-key'
  - 4
  - 4096
  - 2y
  - Add secure passphrase
  - Validated key 'gpg --list-secret-keys --keyid-format SHORT'
   - Key = 97673684
 - Ran 'echo "hello world" | gpg --clearsign'
 - Entered passphrase and saved to keychain
 - Ran 'gpg --armor --export <key>'
 - Created new GPG Key in GitHub using exported public key
  - Settings -> SSH and GPG Keys
 - Local Git GPG settings (set on each GitHub repo)
  - git config user.signingkey 97673684
  - git config commit.gpgSign true
  - git config tag.gpgSign true
  - git config user.email garry@trinder365.co.uk

- GitHub SSH
 - https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
 - ssh-keygen -t ed25519 -C "garry@trinder365.co.uk"
 - Entered passphrase
 - eval "$(ssh-agent -s)"
 - Added to ~/.ssh/config
  - Host github.com
   - AddKeysToAgent yes
   - UseKeychain yes
   - IdentityFile ~/.ssh/id_ed25519
 - ssh-add -K ~/.ssh/id_ed25519
  - Entered passphrase
 - pbcopy < ~/.ssh/id_ed25519.pub

- GitHub CLI
 - gh auth login
  - Complete web browser steps
  - Default git protocol ssh

- GitHub 
 - mkdir github
 - cd GitHub
 - gh repo fork pnp/cli-microsoft365
 - Accept connection prompt - yes
 - Update local git config
  - git config user.signingkey 97673684
  - git config commit.gpgSign true
  - git config tag.gpgSign true
  - git config user.email garry@trinder365.co.uk

  - App Store
   - Microsoft To Do
    - https://apps.apple.com/gb/app/microsoft-to-do/id1274495053?mt=12

- Microsoft Office
 - brew install --cask microsoft-office

- Camtasia
 - brew install --cask camtasia

- Snagit
 - brew install --cask snagit

- iTerm2
 - brew install --cask iterm2
 - Profile
  - Colors 
   - OneTheme
  - Font
   - JetBrains Mono
   - Ligatures Enabled

- OneTheme iTerm2 Theme
 - https://github.com/benniemosher/the-one-theme/
 - Install https://github.com/benniemosher/the-one-theme#iterm-2

- Spaceship Prompt
 - Setup taken from https://garrytrinder.github.io/2020/12/my-wsl2-windows-terminal-setup

- oh-my-zsh
 - sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

- Microsoft Teams
 - https://go.microsoft.com/fwlink/p/?LinkID=869428&clcid=0x809&culture=en-gb&country=GB&lm=deeplink&lmsrc=groupChatMarketingPageWeb&cmpid=directDownloadMac
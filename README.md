# Working with Molecule Semantic Search Repository

## Setup `git`
If you have already setup your git identity, then you can skip this.

Run the following commands to configure your identity. Replace the username and email with your own.
```
git config --global user.name "firstname lastname"
git config --global user.email "youremail@domain.com"
```

## Setup SSH Key For Your GitHub Account

### MacOS

1. **Open Terminal**
1. **Generate SSH Key**: Generate a new SSH key by running the following command. Replace `your_email@example.com` with your GitHub email.
    ```bash
    EMAIL="your_email@example.com"
    ssh-keygen -t ed25519 -C $EMAIL
    ```
1. **Save SSH Key**: When prompted to enter a file to save the key, press Enter to accept the default file location.
1. **Set Passphrase**: Type a secure passphrase when prompted or leave it empty for no passphrase.
1. **Configure SSH-Agent**: Start the SSH agent and add your key to it.
    ```bash
    eval "$(ssh-agent -s)"
    ssh-add --apple-use-keychain ~/.ssh/id_ed25519
    ```  
* Note: If your macOS version is prior to Monterey (12.0), use ssh-add -K ~/.ssh/id_ed25519 instead.
1. **Modify SSH Config**: Check if ~/.ssh/config exists, and create it if it doesn't.
    ```touch ~/.ssh/config
    ``` 
Add the following lines to the file:
    ```Host github.com
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_ed25519
    ```
1. **Copy SSH Key to Clipboard**: Run the following command to copy the public SSH key to your clipboard.
    ```bash
    pbcopy < ~/.ssh/id_rsa.pub
    ```
1. **Add SSH Key to GitHub Account**: 
    - Go to GitHub and log into your account.
    - Click on your profile picture -> Settings -> SSH and GPG keys.
    - Click on the "New SSH key" button and paste your copied public SSH key into the "Key" field.

### Ubuntu Linux

1. **Open Terminal**
1. **Generate SSH Key**: Generate a new SSH key by running the following command. Replace `your_email@example.com` with your GitHub email.
    ```bash
    EMAIL="your_email@example.com"
    ssh-keygen -t rsa -b 4096 -C $EMAIL
    ```
1. **Save SSH Key**: When prompted to enter a file to save the key, press Enter to accept the default file location.
1. **Add SSH Key to SSH-Agent**: Start the SSH agent and add your key to it.
    ```bash
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_rsa
    ```
1. **Copy SSH Key to Clipboard**: Install `xclip` if it's not already installed, and copy the public SSH key to your clipboard.
    ```bash
    sudo apt-get install xclip
    xclip -sel clip < ~/.ssh/id_rsa.pub
    ```
1. **Add SSH Key to GitHub Account**: 
    - Go to GitHub and log into your account.
    - Click on your profile picture -> Settings -> SSH and GPG keys.
    - Click on the "New SSH key" button and paste your copied public SSH key into the "Key" field.

## Make Changes to the `main` Branch via Pull Requests from a Fork

### Why Use Pull Requests?
The `main` branch in the "molecule-semantic-search" repository is protected to maintain the integrity of the code. Direct pushes to this branch are restricted. All changes must be submitted via pull requests to ensure code review and quality control. 

### Merging Strategy
The repository uses a "Squash and Merge" strategy to keep the commit history clean. This strategy combines all the commits from a feature branch into a single commit, which is then added to the main branch.

### Approvals
At least one approver is required to review and approve a pull request before it can be merged into the main branch.

To request an approval, tag Toby and James in the [LinkedIn Group Chat](https://www.linkedin.com/messaging/thread/2-MjJjYTA2NjMtZDYyYS00Y2RhLWE3YzYtNjAwNjQyNzBlZWM4XzAxMw==/).

### How to Make a Pull Request from a Fork

1. **Fork the Repository**: Navigate to the "molecule-semantic-search" GitHub page and click on the "Fork" button at the top-right corner.
1. **Clone Your Fork**: You only need to do this once. Replace `tobkin` with your GitHub username.
    ```bash
    YOUR_USERNAME="tobkin"
    mkdir -p ~/src/valuestreamai
    cd ~/src/valuestreamai
    git clone git@github.com:$YOUR_USERNAME/molecule-semantic-search.git
    ```
    
1. **Add Remote Upstream**: Add the original repository as a remote called "upstream".
    ```bash
    cd ~/src/valuestreamai/molecule-semantic-search
    git remote add upstream git@github.com:valuestreamai/molecule-semantic-search.git
    ```
1. **Fetch Latest Changes**: Sync your fork with the original repository.
    ```bash
    git checkout main
    git fetch upstream
    git merge upstream/main
    ```
1. **Create a New Feature Branch**: Create and check out a new branch named after your associated Linear Issue, e.g., VSA-16.
    ```bash
    BRANCH="VSA-16"
    git checkout -b $BRANCH
    ```
1. **Make Changes**: Edit files as needed for your feature or fix.
1. **Add and Commit Changes**: 
    ```bash
    git add .
    git commit -m "Description of changes"
    ```
1. **Push Changes to Your Fork**: 
    ```bash
    git push origin $BRANCH
    ```
1. **Create a Pull Request**: 
    - Navigate to your fork on GitHub.
    - Click on "Pull Requests" -> "New Pull Request."
    - Choose the base and compare branches, then click "Create Pull Request."
1. **Request Review**: Github will enforce a reviewer requirement to merge your pull request. Tag Toby and James in the [LinkedIn Group Chat](https://www.linkedin.com/messaging/thread/2-MjJjYTA2NjMtZDYyYS00Y2RhLWE3YzYtNjAwNjQyNzBlZWM4XzAxMw==/) to request code review.

1. **Squash and Merge**: Once your pull request is approved, perform a "Squash and Merge" to combine your changes into a single commit before adding them to the main branch.

By following these instructions, you're adhering to the repository's policy of using pull requests to make all changes, ensuring code quality and maintainability.


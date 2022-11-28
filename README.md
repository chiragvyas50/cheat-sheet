## Cheat Sheet
- Terminal Setup
    - Install oh-my-zsh
        ```
        curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh
        ```
    - Install Plugins
        ```
        git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
        git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
        ```
    - Edit `.zshrc`
        ```
        ZSH_THEME="robbyrussell_custome"
        plugins=(
            git
            iterm2
            man
            python
            zsh-syntax-highlighting
            zsh-autosuggestions
        )
        # set autosuggest color
        ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=240'
        # autosuggest accept key
        bindkey '^ ' autosuggest-accept
        ```
    - Enable shorten directory path(Optional: Don't bother about this step if you are going to use Powerlevel9/10k)
        - `cp .oh-my-zsh/themes/robbyrussell.zsh-theme .oh-my-zsh/custom/themes/robbyrussell_custome.zsh-theme`
        - open `.oh-my-zsh/custom/themes/robbyrussell_custome.zsh-theme` and replace `%c --> %~` on second line
        - `exec $SHELL` 
    - Setup Powerlevel10K(Optional)
        - Install: `git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k`
        - Configure: `p10k configure OR exec $SHELL`
- Linux
    |command|description|
    |---|---|
    |grep|grep -RinE 'version' core-r*|
    |reset or printf '\033c' or echo -e \\\\033c|resize the terminal window back to normal after garbage on the screen or screen shrinked in half|
    |replace string in multiple file|grep -RiIl 'master' . \| xargs sed -i "" -e 's/master/primary/I'

- ansible adhoc commands
    ```
    - ansible all -m raw -a "show ip interface brief" -u admin -k -i 10.10.10.10,
    ```
- ansible packaging gotcha
    ```
    - Ansible <= 2.x
        - 2.x (only single version ansible)
    - Ansible 3.x
        - community package(3.x) + ansible-base(>=2.10.6,<2.11)
    - Ansible 4.x
        - community package(4.x) + ansible-core(>=2.11,<2.12)
    Note: 2.11 is when ansible-base is renamed to ansible-core.
    ```
- ssh
    - key based authentication via jump host
    ```
    ssh –A admin@jumphost
    ssh targethost
    ```
    - tunnel
    ```
    ssh -L 4433:10.10.10.10:443 jump_host
    ```
- git
    - delete multiple branches
    ```
    git branch | grep 'keyword' | xargs git branch -d
    ```

    - rebase
    ```
    git checkout your-branch
    git fetch origin master # fetch remote master refs and save it to origin/master
    git rebase origin/master # rebase origin/master into current branch
    git push --force

    OR

    git checkout master
    git pull
    git checkout local_branch_name
    git rebase master
    git push --force # force required if you've already pushed
    ```
- tcpdump
    ```
    sudo tcpdump port 80 -nnS
    sudo tcpdump not src 10.10.10.10 and dst port 80 -nnvvS
    sudo tcpdump port 80 -nnvvS -w pacap.out
    sudo nping -c 1 --tcp -p 80 -g 65000 10.10.10.10
    ```
- netstat
    ```
    sudo netstat -tulpn
    netstat -van | grep 'pid\|3000'
    ```
- aws vpc cloudwatch logs format
    ```
    nacl
        ${version} ${account-id} ${interface-id} ${srcaddr} ${dstaddr} ${pkt-srcaddr} ${pkt-dstaddr} ${srcport} ${dstport} ${protocol} ${packets} ${bytes} ${start} ${end} ${action} ${log-status} ${tcp-flags}
    tgw
        ${version} ${account-id} ${vpc-id} ${subnet-id} ${interface-id} ${srcaddr} ${dstaddr} ${pkt-srcaddr} ${pkt-dstaddr} ${srcport} ${dstport} ${protocol} ${packets} ${bytes} ${start} ${end} ${action} ${log-status} ${tcp-flags}
    ```

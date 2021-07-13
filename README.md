## Cheat Sheet
- Linux
    |command|description|
    |---|---|
    |reset or printf '\033c' or echo -e \\\\033c|resize the terminal window back to normal after garbage on the screen or screen shrinked in half|

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
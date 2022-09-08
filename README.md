# Git Setting Note

## git auto-complete
- copy "C:\Program Files\Git\mingw64\share\git\completion\git-completion.bash" to "C:\Users\$USER$\"
- add line "source ~/git-completion.bash" to "C:\Program Files\Git\etc\bash.bashrc"
- update environment var "HOME" to "C:\Users\$USER$\"


## SSH SHA256 Agent Auto Start
```
SSH_ENV="$HOME/.ssh/env"
function start_agent {
    echo "Initialising new SSH agent..."
    /usr/bin/ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
    echo succeeded
    chmod 600 "${SSH_ENV}"
    . "${SSH_ENV}" > /dev/null
	/usr/bin/ssh-add ~/.ssh/JTengGentexCorp;
}
if [ -f "${SSH_ENV}" ]; then
    . "${SSH_ENV}" > /dev/null
    #ps ${SSH_AGENT_PID} doesn't work under cywgin
    ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
        start_agent;
    }
else
    start_agent;
fi
```

## SSH Multi User Setting
- Setting done in C:\Users\$USER$\.ssh
- Example config file:
```
#personal account
Host personal
	HostName github.com
	User git
	IdentityFile ~/.ssh/$SHA256_KEY_FILE$_NAME_PERSONAL$
	IdentitiesOnly yes

#work account
Host work
	HostName github.com
	User git
	IdentityFile ~/.ssh/$SHA256_KEY_FILE_NAME_WORK$
	IdentitiesOnly yes
```
- Example remote origin setting:
> personal:GitHubUserAccountName/RepoName.git
> work:GitHubUserAccountName/RepoName.git



## git global editor setting
> $ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"


## git remote ssh setup
- https://docs.github.com/en/enterprise-server@3.0/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

## git check lines of code in total
> git diff --stat `git hash-object -t tree /dev/null`


ERROR LOG

5/5/15

1. Won't sh the bootstrap.sh file
- fixed by calling it at the end, oops

2. "update-locale: not found" at line 11 of bootstrap.sh
- because the Codenvy docker base is debian, not ubuntu

3. Switched to ubuntu, error "ADD root/.bashrc /root/.bashrc no rush file or directory"
- just tried removing the line
- Seemed to give me an error even further up about the sudo apt-get - RAM issue?

4. Can't create directory in /home/user/ because I never created a user
- create user commands

5. Warning: application exceeded output range of 116 messages / second
- click on "Show log" while machine is still booting, then you can continue to refresh to follow all the way through

6. "[STDERR] /home/user/application/scripts/bootstrap.sh: 61: 
/home/user/application/scripts/bootstrap.sh: Syntax error: "(" unexpected"
- changed sudo sh to sudo bash when running the script, made sure shebang was on first line

7. [STDERR] psql: could not connect to server: No such file or directory
- Installation of vagrant doesn't happen in bootstrap.sh?
- during the '[STDOUT] finding if posgres user vagrant already exists.' attempt
I believe this is related to #8 so I'm tentatively moving on

8. "[STDERR] debconf: unable to initialize frontend: Dialog
[STDERR] debconf: (Dialog frontend will not work on a dumb terminal, an emacs shell buffer, or without a controlling terminal.)"
- ENV DEBIAN_FRONTEND noninteractive
- suddenly it's throwing a really weird 'error pulling image'

5/6/15

2.9 unable to initialize frontend
It seems likely that we'll encounter 8 - something I'm doing is making these two heavy, and they seem to step on each
others's toes after awhile. But it's working and I'm back to the headless ssl-cert and postgresql-common install.
- tryin ENV DEBIAN_FRONTEND noninteractive
- didn't work

Important to note here that I approached someone about freelancing on this, wait until I hear back and if it's a no continue the search.

5/7/15

3.10 unable to initialize frontend / psql: could not connect to server
Still the same bug as before. I don't know how to diagnose this without running it in a different context and seeing what the prompts are.
I'm at work today so I should be able to attempt this.
- trying to boot on local computer, gave me a git error but we'll see
- 
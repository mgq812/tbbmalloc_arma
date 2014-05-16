To allow 'tbbmalloc for arma' to allocate memory in large page regions, the account, used to run arma,
needs the 'Lock pages in memory' privilege granted.

This can be done manually via secpol.msc or programatically, with this little tool.
(some windows versions don't support secpol.msc, so this tool is the only option)


How to use:

Open a console window with 'Run as Administrator' and type followed by a return:


AddLockMemoryPrivilege useraccountname


Restart your system once!!!!


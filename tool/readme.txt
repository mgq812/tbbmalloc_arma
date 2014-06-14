To allow 'tbbmalloc for arma' to allocate memory in large page regions, the account, used to run arma,
needs the 'Lock pages in memory' privilege granted.

This can be done manually via secpol.msc or programatically, with this little tool.
(some windows versions don't support secpol.msc, so this tool is the only option)

Additional this tool applies the GMF registry tweak (large pages for image file mapping) for arma client. 


How to use:

- find out the name of user account, that is used to run arma (start arma, 'taskmanager'->'processes'->'User Name')

- execute GMF.exe via 'Run as administrator' and type your useraccountname at prompt in the console window     

- press return    

- restart your system     

- enjoy     


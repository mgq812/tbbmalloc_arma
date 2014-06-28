To allow 'tbbmalloc for arma' to allocate memory in large page regions, the account, used to run arma,
needs the 'Lock pages in memory' privilege granted.

This can be done manually via secpol.msc or programatically, with this little tool.
(some windows versions don't support secpol.msc, in this case, this tool is the only option)

Additional this tool applies the GMF registry tweak (large pages for image file mapping) for arma client. 


How to use:

- find out the name of user account, that is used to run arma (start arma, 'taskmanager'->'processes'->'User Name')

- execute LPManager.exe via 'Run as administrator' and type your useraccountname in the white box to the right from 'Privile' button.     

- click 'Privilege' button, there should occure 'Restart!' in the box, in green letters     

- restart your system     

- check the CheckBox 'LP ImageFileMapping Client' to apply the GMF registry tweak for arma3.exe (client)

- enjoy     


To disable GMF tweak, for benchmarking, for example, just use LPManager (as administrator) and uncheck the CheckBox accordingly


IMPORTANT:

Mapping imagefile in large page region normally doesn't work for arma3server.exe (crash at start), because a special flag in servers imagefile header is incompatible with 'UseLargePages'.
But it is possible to make this working for arma server too, if this flag is patched. Normally you have to use 'explorer suite' for such patching.
LPManager is able to apply the required 'DLLCharakteristics' patch in ImageFileHeader and to set the GMF registry tweak for arma3server.exe too, just by checking the related CheckBox.
This implies disabling of ASLR (adress space layout randomization) too, for arma 3 server. 
So please use this only, if you know what this means and what you do!
 
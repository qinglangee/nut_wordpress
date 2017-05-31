# eclipse 删除插件

FAQ How do I remove a plug-in?

Depending upon the particular version of Eclipse you are running with, the difficulty of uninstalling features or plugins from an Eclipse installation ranges from trivial to painful. In some cases, Eclipse doesn't support uninstalling certain 'optional' features after they have been installed.

Run `Help > About Eclipse > Installation Details`, select the software you no longer want and click Uninstall. 
(On Macintosh it is `Eclipse > About Eclipse > Installation Details`.)

In older versions, you might need to Run `Help > Software Updates > Manage Configuration...`, select the feature of interest, and disable it with the task shown in the right window.

'Uninstalling' a feature, using the steps above, disable the feature or plug-in. These steps are using the Update Manager under the covers.

When a feature is disabled, all its plug-ins will be disabled also. They are still available on disk, and they can be enabled at any time in the future.

There is no mechanism within Eclipse to permanently and physically uninstall a feature and its plug-ins. The process to physically and permanently remove an undesirable feature and its plug-ins is a manual process that should be done when Eclipse is not running. In order to do, you will have to manually remove the files there associated with the feature from the eclipse/features directory and its plug-ins from the eclipse/plugins directory. Be very cautious as to which files you delete, and always have a backup of your Eclipse directory. If you remove the wrong files from these directories, you may have quite some trouble restoring your Eclipse to a stable state. Therefore, unless your hard disk storage capacity is extraordinarily limited, it is recommended that you simply leave the physical files in place.

Note that when manually removing plugins as described above, it is likely that some metadata will still cached by Eclipse. This can lead to problems later on. Running Eclipse with the -clean option may help with that, as it causes Eclipse to clean the cached metadata. See the Running Eclipse help page for details about this option.



refs:  
[How do I remove a plug-in?](http://wiki.eclipse.org/FAQ_How_do_I_remove_a_plug-in%3F)  
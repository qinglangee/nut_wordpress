# svn命令行加颜色

下面这个脚本加入到.bashrc中

	#! /bin/bash

	function svn {
	  command svn "$@" | awk '
	  BEGIN {
	    cpt_c=0;
	  }
	  {
	    if        ($1=="C") {
	      cpt_c=cpt_c+1;
	      print "\033[31m" $0 "\033[00m";  # Conflicts are displayed in red
	    }
	    else if   ($1=="A") {
	      print "\033[32m" $0 "\033[00m";  # Add in green
	    }
	    else if   ($1=="?") {
	      print "\033[36m" $0 "\033[00m";  # New in cyan
	    }
	    else if   ($1=="D") {
	      print "\033[35m" $0 "\033[00m";  # Delete in magenta
	    }
	    else if   ($1=="M") {
	      print "\033[31m" $0 "\033[00m";  # Modify in magenta
	    }
	    else if   ($1=="-") {
	      print "\033[31m" $0 "\033[00m";  # Delete line in red
	    }
	    else if   ($1=="+") {
	      print "\033[32m" $0 "\033[00m";  # add line in green
	    }
	    else                {
	      print $0;                        # No color, just print the line
	    }
	  }
	  END {
	    print cpt_c, " conflicts are found.";
	  }';
	}

refs:  
[SVN : Add colors on command-line svn with awk (in bash)](http://stackoverflow.com/questions/8786400/svn-add-colors-on-command-line-svn-with-awk-in-bash)

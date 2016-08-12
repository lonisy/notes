1003  mkdir lilei
1005  cd lilei/
1007  git init
1014  git init lilei2
1016  mkdir lileiself
1021  cd lileiself/
1023  echo "# self" >> README.md
1025  git init
1026  git add README.md
1027  git commit -m "first commit"
1028  git remote add origin https://github.com/lonisy/self.git
1033  vim .git/config
1034  git push -u origin master
1036  touch phpinfo.php
1037  vim phpinfo.php
1038  git add phpinfo.php
1039  git commit -m "submit file "
1040  git push -u origin master
1041  git config --list
1042  git config --global user.name "lonisy"
1043  git config --global user.email lonisy@163.com
1045  echo "<?php phpinfo(); ?>" > phpinfo.php
1046  git add phpinfo.php
1047  git commit -m "submit file "
1048  git status
1049  git push https://lonisy@github.com/lonisy/self.git
1051  mkdir myaes
1052  cd myaes/
1055  touch file
1057  vim file
1059  cd ..
1061  git add myaes/
1062  git commit -m "my files"
1063  git push https://lonisy@github.com/lonisy/self.git



git clone git@114.55.225.47:soho.git

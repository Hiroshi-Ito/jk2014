============
Shell 1
============


実習内容
============
#. shell の機能の理解
#. コマンドの実行
#. 入出力リダイレクションとパイプ
#. history 機能
#. ファイル名の展開・補完機能
#. プリンタの利用


課題
============
history の内容とホームディレクトリにあるファイル(ディレクトリを含む)の詳細情報を上記の順番でプリンタに出力し，提出してください。
氏名，利用コード，演習年月日を忘れずに記入して下さい。  

**ヒント**
  コマンドからの出力をリダイレクションを使ってファイルに書き込んでからプリンタに出力する方法もあります。



実習の手順
============
解説の shell の機能を読んでから始めて下さい。2章にも述べた通り，UNIXでは設定が頻繁に変更され得ます。表示が説明と多少異なっても気にしないようにして下さい。


コマンドの実行
------------ 
シェルはコマンドラインに入力されたコマンドを解釈実行します。::

  pc0486:~% ls -l
  合計 24
  -rw-r--r--    1 a0010985 user         1499 Mar  5 18:04 cal.man
  drwxr-xr-x    2 a0010985 user           96 Mar  5 18:05 doc/
  drwxr-xr-x    3 a0010985 user           96 Apr 10  2002 ns_imap/
  drwx------    2 a0010985 user         8192 Apr 10  2002 nsmail/
  -rw-r--r--    1 a0010985 user          419 Mar  5 18:09 proxy.pac
  drwxr-xr-x    2 a0010985 user           96 Mar  6 15:47 tmp/
  pc0486:~% pwd ; ls -a                         --->  複数のコマンドの連続実行
  /homefsl/a00XX/a00XXXXX/linux   
  ./             .bashrc          .emacs19.el  .netscape/    .xemacs.el  nsmail/
  ../            .canna           .emacs20.el  .newsrc-news  .xinitrc*   proxy.pac
  .Xauthority    .cshrc           .fvwm2rc     .screenrc     .xwm.msgs   tmp/
  .Xdefaults     .emacs           .history     .ssh/         cal.man
  .bash_logout   .emacs-color.el  .kkcrc       .twmrc        doc/
  .bash_profile  .emacs.el        .login       .vine/        ns_imap/


ファイル名の展開・補完
------------
::

  pc0486:~% pwd
  /home/a0001/a00012345/linux
  pc0486:~% cd /usr/bin
  pc0486:bin% pwd
  /usr/bin

/usr/bin というディレクトリには一般ユーザが共通で利用する実行ファイルがたくさんはいっています。::

  pc0486:bin% ls
  GnomeScott*                      mpto*
  Mail@                            mrd@
  R*                               mread@
  X11@                             mren@
  [@                               msgcmp*

      …

  mousetest*                       zmore*
  mpage*                           znew*
  mpartition@                      zsh*
  mpost*                           zsh-3.1.9*

ファイル名の展開機能を使って目的のファイルのみを抽出してみましょう。::

  pc0486:bin% ls w*                   ---> w で始まるファイルを list します。
  w*       weather             which*      wishx*                  wrjpgcom*
  w3m*     weave*              whiptail*   wm-properties-capplet*  wsoundplay*
  wall*    webcontrol_applet*  who*        wmxmms*                 wsoundserver*
  watch*   wftopfa*            whoami*     wnnkill*                wtoc*
  wbinfo*  wget*               whois@      wnnstat*                wx2_conv*
  wc*      whatis*             wish@       wnntouch*
  wddel*   whereami_applet*    wish8.0@    write*
  wdreg*   whereis*            wish8.0jp*  writevt*
  pc0486:bin% ls *z*                  ---> z を含むファイルを list します。
  adnmz*         gettextize*        libtoolize*  protoize*    unzip*       zip*
  bnamazu*       gifrsize*          lnnmz*       psresize*    unzipsfx*    zipcloak*
  bunzip2@       gnome-moz-remote*  lz@          resizecons*  uz*          zipinfo*
  bzcat@         gunzip@            mknmz*       rfnmz*       vfnmz*       zipnote*
  bzgrep*        gzexe*             mzip@        size*        xkibitz      zipsplit*
  bzip2*         gzip@              namazu*      size86@      zcmp*        zless*
  bzip2dir*      gzipdir*           nmz-config*  tgz*         zdiff*       zmore*
  bzip2recover*  immknmz*           nmzgrep*     tknamazu*    zeisstopnm*  znew*
  funzip*        kibitz             pbmtozinc*   tzselect*    zforce*      zsh*
  gcnmz*         kwnmz*             ppmtopuzz*   unprotoize*  zgrep*       zsh-3.1.9*
  pc0486:bin% ls ?b*                 ---> 2番目が b であるファイルをlist します。
  db_archive*     jbibtex*         pbmlife*     pbmtobbnbg*  pbmtolps*    pbmtoybm*
  db_checkpoint*  kbd_mode*        pbmmake*     pbmtocmuwm*  pbmtomacp*   pbmtozinc*
  db_deadlock*    kbdrate@         pbmmask*     pbmtoepsi*   pbmtomgr*    pbmtpg*
  db_dump*        mbadblocks@      pbmpscale*   pbmtoepson*  pbmtopgm*    pbmupc*
  db_dump185*     obgnome-config*  pbmreduce*   pbmtog3*     pbmtopi3*    tbl*
  db_load*        objcopy*         pbmtext*     pbmtogem*    pbmtopk*     wbinfo*
  db_printlog*    objdump*         pbmto10x*    pbmtogo*     pbmtoplot*   xbmtopbm*
  db_recover*     objdump86*       pbmto4425*   pbmtoicon*   pbmtoptx*    ybmtopbm*
  db_stat*        pbm2ppa*         pbmtoascii*  pbmtolj*     pbmtox10bm*
  jbc_applet*     pbmclean*        pbmtoatk*    pbmtoln03*   pbmtoxbm*



文字列のグループでも展開できます。::

  pc0486:bin% ls [w-y]*         ---> w, x, y のいずれかで始まるファイルを list します。
  w*                  whiptail*               wsoundserver*      xsri*
  w3m*                who*                    wtoc*              xvminitoppm*
  wall*               whoami*                 wx2_conv*          xwdtopnm*
  watch*              whois@                  xargs*             yacc*
  wbinfo*             wish@                   xbmtopbm*          ybmtopbm*
  wc*                 wish8.0@                xchat*             yen_applet*
  wddel*              wish8.0jp*              xgettext*          yes*
  wdreg*              wishx*                  ximtoppm*          ypcat*
  weather             wm-properties-capplet*  xkibitz            ypchfn*
  weave*              wmxmms*                 xml-config*        ypchsh*
  webcontrol_applet*  wnnkill*                xmms*              ypmatch*
  wftopfa*            wnnstat*                xmms-config*       yppasswd*
  wget*               wnntouch*               xpmtoppm*          ypwhich*
  whatis*             write*                  xppxp*             yuvsplittoppm*
  whereami_applet*    writevt*                xppxpm*            yuvtoppm*
  whereis*            wrjpgcom*               xpstat
  which*              wsoundplay*             xscreensaver.kss*
  pc0486:bin% ls {co*,rc*}      ---> co か rc で始まるファイルをlist します。
  co*        col*     column*    consolechars@   rcp*          rcs2log*   rcsmerge*
  coco*      colcrt*  comm*      consolehelper*  rcs*          rcsclean*  rcvAppleSingle*
  codepage*  colrm*   compress*  control-panel*  rcs-checkin*  rcsdiff*



~ はホームディレクトリ名に展開されます。::

  pc0486:bin% ls ~
  cal.man  doc/  ns_imap/  nsmail/  proxy.pac  tmp/


ファイル名の補完機能を利用してみましょう。::

  pc0486:bin% ls -l a  ---> a までタイプして Tab を２回タイプすると，候補がlist されます。
  a2p*                  afmtodit*             as86_encap*           audiosend*
  accel*                another_clock_applet* asciitopgm*           aumix*
  access*               any2ps*               asclock_applet*       autoconf*
  aclocal*              anytopnm*             at*                   autoexpect 
  acroread@             apropos*              atktopbm*             autoheader*
  addftinfo*            apt-cache*            atoc_conv*            automake*
  addmodetest*          apt-cdrom*            atod*                 autopasswd 
  addr*                 apt-config*           atof*                 autoreconf*
  addr2line*            apt-get*              atq@                  autoscan*
  addwords@             ar*                   atrm@                 autoupdate*
  adnmz*                as*                   audiocompose*         awk@
  afm2tfm*              as86*                 audiofile-config*     
  pc0486:bin% ls -l awk    ---> aw までタイプして，Tab をタイプすると，候補は1つしか
                                ないので，補完されます。
  lrwxrwxrwx    1 root     root            9 Feb  8  2002 awk -> /bin/gawk*



入出力リダイレクションとパイプ
--------------------------------
ファイルリストの内容を list というファイルに書き込む。::

  pc0486:bin% cd
  pc0486:~% ls -l > list
  pc0486:~% cat list
  合計 32
  -rw-r--r--    1 a0010985 user         1499 Mar  5 18:04 cal.man
  drwxr-xr-x    2 a0010985 user           96 Mar  5 18:05 doc/
  -rw-r--r--    1 a0010985 user            0 Mar  6 15:58 list
  drwxr-xr-x    3 a0010985 user           96 Apr 10  2002 ns_imap/
  drwx------    2 a0010985 user         8192 Apr 10  2002 nsmail/
  -rw-r--r--    1 a0010985 user          419 Mar  5 18:09 proxy.pac
  drwxr-xr-x    2 a0010985 user         8192 Mar  6 15:55 tmp/
  pc0486:~% ls -l
  合計 40
  -rw-r--r--    1 a0010985 user         1499 Mar  5 18:04 cal.man
  drwxr-xr-x    2 a0010985 user           96 Mar  5 18:05 doc/
  -rw-r--r--    1 a0010985 user          450 Mar  6 15:58 list
  drwxr-xr-x    3 a0010985 user           96 Apr 10  2002 ns_imap/
  drwx------    2 a0010985 user         8192 Apr 10  2002 nsmail/
  -rw-r--r--    1 a0010985 user          419 Mar  5 18:09 proxy.pac
  drwxr-xr-x    2 a0010985 user         8192 Mar  6 15:55 tmp/

list というファイルができています。
このファイルに ps の内容を追加書きしましょう。::

  pc0486:~% ps
    PID TTY          TIME CMD
   1059 ttyp1    00:00:00 tcsh
   5916 ttyp1    00:00:00 ps
  pc0486:~% ps >> list
  pc0486:~% cat list
  合計 32
  -rw-r--r--    1 a0010985 user         1499 Mar  5 18:04 cal.man
  drwxr-xr-x    2 a0010985 user           96 Mar  5 18:05 doc/
  -rw-r--r--    1 a0010985 user            0 Mar  6 15:58 list
  drwxr-xr-x    3 a0010985 user           96 Apr 10  2002 ns_imap/
  drwx------    2 a0010985 user         8192 Apr 10  2002 nsmail/
  -rw-r--r--    1 a0010985 user          419 Mar  5 18:09 proxy.pac
  drwxr-xr-x    2 a0010985 user         8192 Mar  6 15:55 tmp/
    PID TTY          TIME CMD
   1059 ttyp1    00:00:00 tcsh
   5917 ttyp1    00:00:00 ps

list のファイルの内容を wc にリダイレクトします。 ::

  pc0486:~% wc < list          ---> wc コマンドでlistの行数，ワード数，文字数を調べる。
       11      77     534


パイプ機能を使って，PAGER を利用します。::

  pc0486:~% pr list                ---> list の内容を表示します。

  ながれて読めない…


  pc0486:~% pr list | more


  2003-03-06 15:59                     list                       ページ    1


  合計 32
  -rw-r--r--    1 a0010985 user         1499 Mar  5 18:04 cal.man
  drwxr-xr-x    2 a0010985 user           96 Mar  5 18:05 doc/
  -rw-r--r--    1 a0010985 user            0 Mar  6 15:58 list
  drwxr-xr-x    3 a0010985 user           96 Apr 10  2002 ns_imap/
  drwx------    2 a0010985 user         8192 Apr 10  2002 nsmail/
  -rw-r--r--    1 a0010985 user          419 Mar  5 18:09 proxy.pac
  drwxr-xr-x    2 a0010985 user         8192 Mar  6 15:55 tmp/
    PID TTY          TIME CMD
   1059 ttyp1    00:00:00 tcsh
   5917 ttyp1    00:00:00 ps


















  --続ける--                             ---> Space キーで次頁へ







historyの機能
-----------------
``history`` コマンドを実行すると，環境変数 HISTSIZE に設定されている数（本演習の設定では1000 個）を上限としてコマンドの履歴が表示されます。::

  pc0486:~% history
       1  15:49:24        pwd
       2  15:49:28        cd /usr/bin
       3  15:49:36        pwd
       4  15:49:52        ls
       5  15:50:24        ls | more
       6  15:51:31        ls w*
       7  15:51:44        ls *b*
       8  15:51:56        ls w*

      …

      32  15:59:28        ps >> list
      33  15:59:32        cat list
      34  15:59:44        wc < list
      35  16:00:06        pr list
      36  16:00:22        pr list | more
      37  16:00:55        history

このリストを使ってコマンドを実行します。::

  pc0486:~% !!                              ---> 直前のコマンドの再実行
  history
       1  15:49:24        pwd
       2  15:49:28        cd /usr/bin
       3  15:49:36        pwd
       4  15:49:52        ls
       5  15:50:24        ls | more
       6  15:51:31        ls w*
       7  15:51:44        ls *b*
       8  15:51:56        ls w*

      …

      32  15:59:28        ps >> list
      33  15:59:32        cat list
      34  15:59:44        wc < list
      35  16:00:06        pr list
      36  16:00:22        pr list | more
      37  16:00:55        history
      38  16:01:23        history


番号や文字列でも指定できます。::

  pc0486:~% !1                           ---> 1番目の命令を再度実行
  pwd
  /home/linux
  pc0486:~% !w                           ---> wで始まる最新の命令を再度実行
  wc < list 
       11      77     534

``C-p``，``C-n`` を使って，コマンド履歴を呼び出します。::

  pc0486:~%                 C-pと入力   ---> 一つ前のコマンドがコマンドラインに出る
  pc0486:~% wc < list
         % pwd              C-pを繰り返すと遡っていく
         % history          C-p 
         % history          C-p
         % pr list | more   C-p
         % history          C-nとすると逆にたどる
         % history          C-n
         % pwd              C-n
         % wc < list        C-f C-b で移動  del などで編集，リターンで実行
  pc0486:~% wc -l < list    wc に オプション -l を付加して実行してみます
       11


解説
======


.. _shell:

shellの機能
--------------

#. ユーザが入力したコマンドを解釈実行するプログラム(コマンドインタープリタ)をUNIXでは **shell** と呼びます。UNIXの一番外側を覆っているというイメージです。

#. shell はユーザインターフェイス，環境設定，シェルプログラミングの役割を持ちます。

#. UNIX にはいくつかの種類のshellがあります。 ``B shell[sh]`` , ``C shell[csh]`` , ``TC shell[tcsh]`` , ``bash`` などです [#shell1]_ 。実際，shell によって使い勝手が変り，ユーザにとってはshellすなわちUNIXと感じられることが往々にしてあります。UNIXではユーザは好きなshell を選べます。本演習では ``bash`` を利用しています。


#. X windowでは各々のターミナルウィンドウに shell が起動されています。





コマンドの実行
-------------
\subsubsection{説 明}
\begin{enumerate}
\item 端末にプロンプトを表示して，ユーザの入力を待っています。
これは，
入力促進記号と言い，
shellが命令の解析準備が出来，入力待ちをしていることを示すものです。
%
\item 改行までをコマンド行として読み込みます
\footnote{会話形式ではキーボードからのみならず，
ファイルからの読み込みも可能です。}。
%
\end{enumerate}

%
\subsubsection{実行例}

%シェルのバージョンを見てみましょう。
%\begin{center}
%\begin{shadebox}
%\begin{verbatim}
%pc0486:~% echo $version
%tcsh 6.10.00 (Astron) 2000-11-19 (i386-intel-linux) options 8b,nls,dl,al,kan,rh,color,
%dspm
%\end{verbatim}
%\end{shadebox}
%\end{center}
複数のコマンドの連続実行を行います。
\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% pwd ; ls -a
/home/linux
./             .bashrc          .emacs19.el  .netscape/    .xemacs.el  nsmail/
../            .canna           .emacs20.el  .newsrc-news  .xinitrc*   proxy.pac
.Xauthority    .cshrc           .fvwm2rc     .screenrc     .xwm.msgs   tmp/
.Xdefaults     .emacs           .history     .ssh/         doc/        userlist
.bash_logout   .emacs-color.el  .kkcrc       .twmrc        list
.bash_profile  .emacs.el        .login       .vine/        ns_imap/
pc0486:~% which pwd
/bin/pwd
pc0486:~% ls -l `which pwd`
-rwxr-xr-x    1 root     root         7148 Jul 21  2000 /bin/pwd*
\end{verbatim}
\end{shadebox}
\end{center}
連続実行の際に複数のコマンドを
まとめて1つのコマンドのように実行したい場合には\verb|( )|で括ります。

あるコマンドの出力結果をコマンドラインの一部として使いたい時は，
そのコマンドをバッククオートで括ります。
これをコマンドの展開といいます。

\subsection{コマンドラインでの編集}

\subsubsection{説明}

コマンドの入力中に誤って入力した時，
まだ実行していなければ，
コマンドライン上で編集し直すことができます。
この時の編集キー操作は，
以下の表のようになっています
\footnote{
%2007% 初期設定は emacs モード( mule と同じ)となっているので，
%2007% mule のキーバインディングと同じです。
初期設定はemacs モード となっているので，
emacs のキーバインディングと同じです。
}。

\begin{table}[h]
\begin{center}
\begin{tabular}{|c|l||c|l|} \hline \hline
\verb+C-b+ & 一文字左へカーソルを移動 & 
\verb+C-f+ & 一文字右へカーソルを移動 \\
\verb+C-a+ & 行の先頭へカーソルを移動 &
\verb+C-e+ & 行の末尾へカーソルを移動 \\
\verb+C-d+ & カーソル位置の一文字を削除 &
\verb+C-k+ & カーソル位置から行末までを削除 \\ \hline
\end{tabular}
\end{center}
\end{table}

%\subsubsection{実行例}
%
%\begin{center}
%\begin{shadebox}
%\begin{verbatim}
%pc0486:~% cd /
%pc0486:/% ls
%admin/  boot/  etc/   kyoto/  lost+found/  mnt/  patch/  root/  site/   tmp/  var/
%bin/    dev/   home/  lib/    misc/        opt/  proc/   sbin/  staff/  usr/
%pc0486:/% ls us
%              ：ここで[Tab] キーを押すと us のつくのは usr しかないので
%                以下のように補完されます。
%pc0486:/% ls usr/
%Hwork/  dict/  games/              include/  libexec/     man/    src/
%X11R6/  doc/   i386-redhat-linux/  info/     local/       sbin/   tmp@
%bin/    etc/   i486-linux-libc5/   lib/      lost+found/  share/  vine/
%pc0486:/% ls v
%              ：ここで[C-d] キーを押すと v のつくファイルの候補が
%                以下のように表示されます。
%var/ 
%pc0486:/% ls var/
%cache/  lib/    lock/  man2html/  namazu/  preserve/  samba/  ssl/    tmp/
%db/     local/  log/   mars_nwe/  nis/     run/       spool/  state/  yp/
%\end{verbatim}
%\end{shadebox}
%\end{center}


\subsection{history機能}
\subsubsection{説明}
ユーザが過去にキーボードから入力したものを記憶しておき，
必要なときに呼び出す機能がhistory機能です。
同じようなコマンドを何度も入力したい時などはとても便利です。
history機能を使うには，
入力したコマンド行を記憶しておかなくてはなりません。
この記憶しておく行の数の
%2007% 上限をシェル変数 \verb|history| でセットします
上限を、環境変数と呼ばれる変数 HISTSIZE でセットします
%2007% \footnote{シェル変数については，shell 2 で詳しく解説します。}
。
%2007% また，history機能にはlogoutした時のhistoryの内容を
%2007% シェル変数 \verb|savehist| の値だけ，
%2007% 次のlogin 時に引き継ぐ機能もあります。

%2007%   set history=100   :100個の履歴を保存します
%2007%   set savehist=50  :50個の履歴を次のログイン時まで引き継ぎます
\begin{verbatim}
   HISTSIZE=100 ：100個の履歴を保存します
\end{verbatim}

\fbox{\verb+C-p+} で直前のコマンドラインが現れます。
さらに，\fbox{\verb+C-p+} を押していくと，
次々に古い履歴に遡っていきます。
逆に \fbox{\verb+C-n+} で元に戻っていきます。
コマンドラインが現れている状態で，
必要ならば，コマンドラインでの編集を行って，
\keytop{\verb|Return|} で実行します。

また，
\verb|history| とすれば%2007%\verb|tcsh| の
保存しているコマンドの履歴が見られます。
この左端の番号は，通し番号で，
これを用いてコマンド行の参照を行います。
コマンド行の参照は，\keytop{\verb+!+}を使います(イベント置換)。

%
\begin{itembox}{イベント置換}
\begin{center}
\begin{verbatim}
   !!   : 直前のコマンドライン
   !num : 番号のコマンドライン
   !-n  : n 回前のコマンドライン
   !str : 先頭の文字列がstrのコマンドラインでもっとも新しいもの
\end{verbatim}
\end{center}
\end{itembox}
%
\subsubsection{実行例}

\verb|history| を実行すると，過去のコマンドの履歴のリストが表示されます。

\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:/% cd
pc0486:~% history
     1  15:49:24        pwd
     2  15:49:28        cd /usr/bin
     3  15:49:36        pwd
     4  15:49:52        ls
     5  15:50:24        ls | more
     6  15:51:31        ls w*
     7  15:51:44        ls *b*
     8  15:51:56        ls w*

    …

    32  15:59:28        ps >> list
    33  15:59:32        cat list
    34  15:59:44        wc < list
    35  16:00:06        pr list
    36  16:00:22        pr list | more
    37  16:00:55        history
\end{verbatim}
\end{shadebox}
\end{center}
イベント置換機能を使って，過去のコマンドを使います。
番号による利用，文字列による利用ができます。
\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% !!                              ---> 直前のコマンドの再実行
history
     1  15:49:24        pwd
     2  15:49:28        cd /usr/bin
     3  15:49:36        pwd
     4  15:49:52        ls
     5  15:50:24        ls | more
     6  15:51:31        ls w*
     7  15:51:44        ls *b*
     8  15:51:56        ls w*

    …

    32  15:59:28        ps >> list
    33  15:59:32        cat list
    34  15:59:44        wc < list
    35  16:00:06        pr list
    36  16:00:22        pr list | more
    37  16:00:55        history
    38  16:01:23        history
pc0486:~% !1
pwd
/home/linux
pc0486:~% !w
wc < list 
     11      77     534
\end{verbatim}
\end{shadebox}
\end{center}
前節で説明した通り，
後で利用するエディタの emacs と同じ \keytop{\verb|Ctrl|} を利用したキー操作で，
過去のコマンドをコマンドラインに表示させて，
これを編集して実行することができます。
同じコマンドを適用するファイル名だけ変えたい時や，
オプションだけ変更したい時などに便利です。
\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~%                 C-pと入力   ---> 一つ前のコマンドがコマンドラインに出る
pc0486:~% wc < list
        % pwd              C-pを繰り返すと遡っていく
        % history          C-p 
        % history          C-p
        % pr list | more   C-p
        % history          C-nとすると逆にたどる
        % history          C-n
        % pwd              C-n
        % wc < list        C-f C-b で移動  del などで編集，リターンで実行
pc0486:~% wc -l < list    wc に オプション -l を付加して実行してみます
     11
\end{verbatim}
\end{shadebox}
\end{center}


\subsection{ファイル名の展開・補完}
\subsubsection{説明}

シェルでは，ファイル名の指定が簡単に行なえるように
「ファイル名の展開」と言う機能を提供しています。
この機能は，コマンド行でファイル名を指定するとき，
ある{\bf パターン}を指定するとシェルがその部分をパターンに一致する
全てのファイル名に置き換えてくれると言うものです。

この機能は使えば，ホームディレクトリにある ``h''の文字で始まる
ファイルの情報を表示させることなども簡単にできます。

以下にパターンを指定するのに用いる特殊文字を示しておきます。\\[1zw]
%
\begin{itembox}{ファイル名の展開に使う特殊文字}

\begin{center}
\begin{tabular}{c@{\ :\ }p{12cm}}
\verb+?+ & 任意の一文字 \\
\verb+*+ & 任意の文字列 (空文字列を含む)\\
\verb+[ ]+ &文字クラス

\verb+[ ]+で囲まれた中にある一文字。
文字クラスは\verb+-+で区切って範囲を指定。

\verb+[0-9] = [0123456789]+,
\verb+[a-dh-k] = [abcdhijk]+ \\

\verb+~+ & ホームディレクトリ\\
\verb+~user + & ユーザ名userのホームディレクトリ
\end{tabular}\\[0.5zw]
\end{center}
\end{itembox}

%
%さらに，\verb+tcsh+ では \keytop{\verb+Tab+} でファイル名補完
%\footnote{ファイル名を途中まで入力し，
%\protect\keytop{\verb+Tab+} を打つとそれに続くファイル名を補完してくれます。}，
%\fbox{\verb+C-d+} で補完候補一覧が表示されます。

\subsubsection{実行例}

例えばたくさんのファイルが格納されているディレクトリの中から，
目的のファイルを探すのは骨がおれます。
\verb|/usr/bin| には，
利用者が共通に使う多くのコマンド類が収められています。
\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% cd /usr/bin
pc0486:bin% ls
GnomeScott*                      mpto*
Mail@                            mrd@
R*                               mread@
X11@                             mren@
[@                               msgcmp*

    …

mousetest*                       zmore*
mpage*                           znew*
mpartition@                      zsh*
mpost*                           zsh-3.1.9*
\end{verbatim}
\end{shadebox}
\end{center}

確か\verb|w|で始まるコマンドだったんだが，
思い出せない時は，次のようにします。
\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:bin% ls w*
w*       weather             which*      wishx*                  wrjpgcom*
w3m*     weave*              whiptail*   wm-properties-capplet*  wsoundplay*
wall*    webcontrol_applet*  who*        wmxmms*                 wsoundserver*
watch*   wftopfa*            whoami*     wnnkill*                wtoc*
wbinfo*  wget*               whois@      wnnstat*                wx2_conv*
wc*      whatis*             wish@       wnntouch*
wddel*   whereami_applet*    wish8.0@    write*
wdreg*   whereis*            wish8.0jp*  writevt*
\end{verbatim}
\end{shadebox}
\end{center}
他の例も見てみましょう。
\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:bin% ls [w-y]*
w*                  whiptail*               wsoundserver*      xsri*
w3m*                who*                    wtoc*              xvminitoppm*
wall*               whoami*                 wx2_conv*          xwdtopnm*
watch*              whois@                  xargs*             yacc*
wbinfo*             wish@                   xbmtopbm*          ybmtopbm*
wc*                 wish8.0@                xchat*             yen_applet*
wddel*              wish8.0jp*              xgettext*          yes*
wdreg*              wishx*                  ximtoppm*          ypcat*
weather             wm-properties-capplet*  xkibitz            ypchfn*
weave*              wmxmms*                 xml-config*        ypchsh*
webcontrol_applet*  wnnkill*                xmms*              ypmatch*
wftopfa*            wnnstat*                xmms-config*       yppasswd*
wget*               wnntouch*               xpmtoppm*          ypwhich*
whatis*             write*                  xppxp*             yuvsplittoppm*
whereami_applet*    writevt*                xppxpm*            yuvtoppm*
whereis*            wrjpgcom*               xpstat
which*              wsoundplay*             xscreensaver.kss*
pc0486:bin% ls {co*,rc*}
co*        col*     column*    consolechars@   rcp*          rcs2log*   rcsmerge*
coco*      colcrt*  comm*      consolehelper*  rcs*          rcsclean*  rcvAppleSingle*
codepage*  colrm*   compress*  control-panel*  rcs-checkin*  rcsdiff*
\end{verbatim}
\end{shadebox}
\end{center}
このように特殊文字を使ってさまざまに展開できます。
多くのデータファイルを保存する時，
この機能を考慮して名前をつけると整理が便利になります。

ファイル名の補完機能も良く利用します。
入力の途中で \keytop{\verb|Tab|} を２回タイプすると，
入力した所までの文字列にマッチするファイルをリストアップします。
これから選んで実行します。
マッチするファイルが1つしかない時，
\keytop{\verb|Tab|} をタイプすると，完全に補完されます。
この時2つ以上候補があると，ブザーが鳴ります。
\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:bin% ls -l a      ---> C-d とタイプする。
a2p*                  afmtodit*             as86_encap*           audiosend*
accel*                another_clock_applet* asciitopgm*           aumix*
access*               any2ps*               asclock_applet*       autoconf*
aclocal*              anytopnm*             at*                   autoexpect 
acroread@             apropos*              atktopbm*             autoheader*
addftinfo*            apt-cache*            atoc_conv*            automake*
addmodetest*          apt-cdrom*            atod*                 autopasswd 
addr*                 apt-config*           atof*                 autoreconf*
addr2line*            apt-get*              atq@                  autoscan*
addwords@             ar*                   atrm@                 autoupdate*
adnmz*                as*                   audiocompose*         awk@
afm2tfm*              as86*                 audiofile-config*     
pc0486:bin% ls -l awk    ---> aw までタイプして，Tab をタイプする。
lrwxrwxrwx    1 root     root            9 Feb  8  2002 awk -> /bin/gawk*
\end{verbatim}
\end{shadebox}
\end{center}


\subsection{入出力リダイレクションとパイプ}
\label{sec:red}

\subsubsection{説 明}
シェルはコマンドの入力や出力を切り換える機能を持っています。
この機能を入出力リダイレクション機能と言います。
プロセスには，入出力を行うための標準的な機器が定義されています。
それらは標準入力(\verb+stdin+)，標準出力(\verb+stdout+)，
標準エラ−出力(\verb+stderr+)と呼ばれています。
これらは各々キ−ボ−ド，コンソ−ル，コンソ−ルに割り当てられています。
この設定のために，コマンドを実行すると
その実行結果はコンソ−ルに表示されます。
しかし，実行結果をファイルに残したい場合がありますが，
この様な場合，UNIXでは標準入出力をファイルに置き換えることができます。\\[1zw]
%
\begin{itembox}{入出力リダイレクション}
\begin{center}
\begin{tabular}{ll}
%\rule[-0.3zw]{0.0mm}{1.5zw}
標準入力の切り換え & \verb+command < + filename \\
標準出力の切り換えA & \verb+command > + filename \\
標準出力の切り換えB & \verb+command >> + filename \\
標準出力および標準エラ−出力の切り換えA & \verb+command >& + filename \\
標準出力および標準エラ−出力の切り換えB & \verb+command >>& + filename \\
\end{tabular} 
\end{center}
\end{itembox}
%
出力切り換えのAは新しいファイルを作成してその中に書き込む場合であり，
%この場合に既に存在するファイルを指定するとエラ−になる。
Bは指定したファイルが無ければ作成し，
存在すればそのファイルに追加して書き込む場合です。

パイプライン機能は，パイプ演算子``\verb+|+''を
含むコマンド行で指定し，この左側のコマンドの標準出力を
右側の標準入力につなぐ働きをします。
UNIXのコマンドの中には，標準入力からデータを受け取り
処理して標準出力に出すものが多くあります
\footnote{この様なプログラムをフィルタと呼びます。}。
このパイプ機能を利用すれば既存のコマンドをパイプを用いてつなぎ合わせることで
新しい多機能のコマンドが作れます。
%

\subsubsection{実行例}

\texttt{list} というファイルを作って書き込む。
標準出力を切替えます。

\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% ls -l > list
pc0486:~% cat list
合計 32
-rw-r--r--    1 a0010985 user         1499 Mar  5 18:04 cal.man
drwxr-xr-x    2 a0010985 user           96 Mar  5 18:05 doc/
-rw-r--r--    1 a0010985 user            0 Mar  6 15:58 list
drwxr-xr-x    3 a0010985 user           96 Apr 10  2002 ns_imap/
drwx------    2 a0010985 user         8192 Apr 10  2002 nsmail/
-rw-r--r--    1 a0010985 user          419 Mar  5 18:09 proxy.pac
drwxr-xr-x    2 a0010985 user         8192 Mar  6 15:55 tmp/
\end{verbatim}
\end{shadebox}
\end{center}

\texttt{ps} の出力内容をファイル\verb|list|に追加書きします。

\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% ps >> list
pc0486:~% cat list
合計 32
-rw-r--r--    1 a0010985 user         1499 Mar  5 18:04 cal.man
drwxr-xr-x    2 a0010985 user           96 Mar  5 18:05 doc/
-rw-r--r--    1 a0010985 user            0 Mar  6 15:58 list
drwxr-xr-x    3 a0010985 user           96 Apr 10  2002 ns_imap/
drwx------    2 a0010985 user         8192 Apr 10  2002 nsmail/
-rw-r--r--    1 a0010985 user          419 Mar  5 18:09 proxy.pac
drwxr-xr-x    2 a0010985 user         8192 Mar  6 15:55 tmp/
  PID TTY          TIME CMD
 1059 ttyp1    00:00:00 tcsh
 5917 ttyp1    00:00:00 ps
\end{verbatim}
\end{shadebox}
\end{center}

標準入力をファイルに切替えてみましょう。
\verb+wc+ コマンドでファイル \texttt{list} の行数，
ワード数，文字数を調べます。
%
\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% wc < list
     11      77     534
\end{verbatim}
\end{shadebox}
\end{center}
11行，77ワード，534文字のファイルであることがわかります。

パイプ機能を使って，同様の作業を行います。
この時 \texttt{list} というファイルは作らずにできます。
データがパイプを通って，コマンドからコマンドに渡ります。
\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% cat list | wc
     11      77     534
pc0486:~% ls -al | wc
     36     317    2325
\end{verbatim}
\end{shadebox}
\end{center}

\verb|pr| コマンドでファイル \verb|list| を画面に表示してみましょう。
\verb|pr| コマンドでは，内容が一画面を越えて流れてしまいます。
これをパイプ機能を使って，\texttt{more} コマンドにつなぎ，
一画面毎に止めてみます。

\begin{center}
\begin{minipage}{15cm}
\begin{footnotesize}
\begin{screen}
\begin{verbatim}

pc0486:~% pr list 

ながれて読めないよ…

\end{verbatim}
\end{screen}
\end{footnotesize}
\end{minipage}
\end{center}

\begin{center}
\begin{minipage}{15cm}
\begin{footnotesize}
\begin{screen}
\begin{verbatim}
pc0486:~% pr list | more


2003-03-06 15:59                     list                       ページ    1


合計 32
-rw-r--r--    1 a0010985 user         1499 Mar  5 18:04 cal.man
drwxr-xr-x    2 a0010985 user           96 Mar  5 18:05 doc/
-rw-r--r--    1 a0010985 user            0 Mar  6 15:58 list
drwxr-xr-x    3 a0010985 user           96 Apr 10  2002 ns_imap/
drwx------    2 a0010985 user         8192 Apr 10  2002 nsmail/
-rw-r--r--    1 a0010985 user          419 Mar  5 18:09 proxy.pac
drwxr-xr-x    2 a0010985 user         8192 Mar  6 15:55 tmp/
  PID TTY          TIME CMD
 1059 ttyp1    00:00:00 tcsh
 5917 ttyp1    00:00:00 ps















--続ける--
\end{verbatim}
\end{screen}
\end{footnotesize}
\end{minipage}
\end{center}


\subsection{特殊文字のエスケープ(クオート)}

\subsubsection{バッククオート}

あるコマンドの出力結果をコマンドラインの一部として使いたい時は，
そのコマンドをバッククオートで括ります。

\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% which pwd
/bin/pwd
pc0486:~% ls -l `which pwd`
-rwxr-xr-x    1 root     root         7148 Jul 21  2000 /bin/pwd*
\end{verbatim}
\end{shadebox}
\end{center}

\subsubsection{バックスラッシュ，シングルクオート，ダブルクオート}

コマンドラインの文字の中で，
コマンドに渡される文字と
コマンドが解釈する文字(特殊文字)があります。
この特殊文字を\verb+tcsh +のメタキャラクタといいます。
たとえば，\verb+I/O+ リダイレクションで使う \verb+ <, >, &+ などです。

これらを解釈されないようにすることを
エスケープするといいます。
これには，
文字の前にバックスラッシュ \verb+ \+ をつけるか，
あるいは，
シングルクオート \fbox{'} かダブルクオート\fbox{”}
で囲みます。 

\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% ls > ?.doc            ： ?.doc というファイルを作ってみましょう。
?.doc: 照合パターンに合いません.
pc0486:~% ls > \?.doc           ： こうすれば，
pc0486:~% ls
?.doc  doc/  list  ns_imap/  nsmail/  proxy.pac  tmp/
pc0486:~% rm \?.doc             ： 消す時も
rm: `?.doc' を削除しますか(yes/no)? y
pc0486:~% ls
doc/  list  ns_imap/  nsmail/  proxy.pac  tmp/
pc0486:~% echo my name is $user
my name is a0010985
pc0486:~% echo 'my name is $user'
my name is $user
pc0486:~% echo "my name is $user"
my name is a0010985
\end{verbatim}
\end{shadebox}
\end{center}
シングルクオートで囲んだ時は，シェル変数や環境変数は展開されませんが，
ダブルクオートで囲んだ時は展開されます。

%\clearpage
間違って \verb+ -a+
というファイルを作ってしまいました。
どうして消しましょうか。

\begin{center}
\begin{shadebox}
\begin{verbatim}
pc0486:~% ls > -a
pc0486:~% ls
-a  doc/  list  ns_imap/  nsmail/  proxy.pac  tmp/
pc0486:~% rm -a
rm: オプションが違います -- a
詳しくは `rm --help' を実行して下さい.
pc0486:~% less -a
Missing filename ("less --help" for help)
pc0486:~% pwd
/home/linux
pc0486:~% rm ~/-a
rm: `/home/linux/-a' を削除しますか(yes/no)? y
pc0486:~% ls
doc/  list  ns_imap/  nsmail/  proxy.pac  tmp/
\end{verbatim}
\end{shadebox}
\end{center}





.. rubric:: 脚注
.. [#shell1] shell を変更したいときは ``chsh`` コマンドを使います。（現在使用不可）











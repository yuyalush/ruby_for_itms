===========================
クラウドコンピューティング
===========================

正しくクラウドコンピューティングを理解しましょう
--------------------------------------------------

スライド参照


実践・ニフティクラウド
===========================


ログイン・キーファイルの取得
----------------------------------------

以下のURLにアクセスをして、コントロールパネルへログインします。

http://cloud.nifty.com/

.. image:: images/01_login.png

配布されたIDとPasswordを入力する

.. image:: images/02_login_input.png


SSHのキー作成を行う。

.. image:: images/03_ssh.png

キーのダウンロードが行われるので、どこに保存されているか確認しておくこと。

.. image:: images/04_keydownload.png


FireWallのプラン変更
----------------------------------------

今回はRailsの動作確認で使うサーバのために、独自の設定を行います。
そのため、Firewallは有償プランにて行って頂きます。

ファイアーウォールのメニューに入る

.. image:: images/01_fire.png

有償プランへ変更する

.. image:: images/02_fire.png

.. image:: images/03_fire.png


サーバーの作成
----------------------------------------

サーバ作成画面へ

.. image:: images/05_server.png

CentOS 5.6 Plainを選択する

.. image:: images/06_plain.png

サーバ名を入力

.. image:: images/07_servername.png

miniを選択する

.. image:: images/08_mini.png

料金は従量を選択する

.. image:: images/09_price.png

sshキーを選ぶ

.. image:: images/10_sshkey.png

Firewallの設定を行います

.. image:: images/11_firewall.png

.. image:: images/12_firewall2.png

最後に確認し、作成する。

.. image:: images/13_result1.png

.. image:: images/14_result2.png

.. image:: images/15_servercreated.png



teratermで接続
----------------------------------------

.. image:: images/ssh0.png

.. image:: images/ssh1.png



セットアップ
---------------------------

基本のシェルは以下のURLになります。

https://gist.github.com/1176137


以下をコピー＆ペーストして下さい。

curl  https://gist.github.com/raw/1176137/5357fb0721c44bf810f9747101d29465b7c03a1d/setup2.sh | sh




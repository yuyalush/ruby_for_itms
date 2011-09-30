===========================
クラウドコンピューティング
===========================

正しくクラウドコンピューティングを理解しましょう
----------------------------------------------------


ニフティクラウドについて
---------------------------


実践・ニフティクラウド
===========================


ログイン・キーファイルの取得
========================================

以下のURLにアクセスをして、コントロールパネルへログインします。

http://cloud.nifty.com/

.. image:: pic/01_login.png

配布されたIDとPasswordを入力する

.. image:: pic/02_login_input.png


SSHのキー作成を行う。

.. image:: pic/03_ssh.png

キーのダウンロードが行われるので、どこに保存されているか確認しておくこと。

.. image:: pic/04_keydownload.png


FireWallのプラン変更
========================================

今回はRailsの動作確認で使うサーバのために、独自の設定を行います。
そのため、Firewallは有償プランにて行って頂きます。

ファイアーウォールのメニューに入る

.. image:: pic/01_fire.png

有償プランへ変更する

.. image:: pic/02_fire.png

.. image:: pic/03_fire.png


サーバーの作成
==============================

サーバ作成画面へ

.. image:: pic/05_server.png

CentOS 5.6 Plainを選択する

.. image:: pic/06_plain.png

サーバ名を入力

.. image:: pic/07_servername.png

miniを選択する

.. image:: pic/08_mini.png

料金は従量を選択する

.. image:: pic/09_price.png

sshキーを選ぶ

.. image:: pic/10_sshkey.png

Firewallの設定を行います

.. image:: pic/11_firewall.png

.. image:: pic/12_firewall2.png

最後に確認し、作成する。

.. image:: pic/13_result1.png

.. image:: pic/14_result2.png

.. image:: pic/15_servercreated.png



teratermで接続
==============================

.. image:: pic/ssh0.png

.. image:: pic/ssh1.png



こんなこともできます
---------------------------


クラウドコンピューティングがもたらす世界
----------------------------------------



多様化するクラウドコンピューティング
----------------------------------------



==============================
CRMを作ってみよう！
==============================


easyCRM
==============================


easyCRMの構成
==============================

.. image:: pic/easyCRM_ER.png

easyCRMは非常に単純なCRMです。
管理する項目は以下の３つです。

* Company(会社)
* Customer(顧客)
* Staff(社員)

顧客は会社に属します。
社員は顧客を担当します。
一人の顧客に対して一人の社員が担当となります。

Company(会社)
------------------------------


easyCRMの特徴
------------------------------


easyCRM構築作業
-----------------------------

まずはアプリケーションのベースを生成します。

.. code-block:: bash
    :linenos:

    % rails new easyCRM
    % cd easyCRM
    % rails s

ctrl+cでサーバを止める。

.. code-block:: bash
    :linenos:

    % rails g scaffold Staff name:string section:string
    % rake db:migrate
    % rails s

以上です。これでベースと社員に関する処理が出来る状態になっています。
http:// IPアドレス /staffs/ にアクセスして下さい。


.. code-block:: bash
    :linenos:

    コントローラーを見てみる
    % nano app/controller/staffs_controller.rb

    ヴューを見てみる
    Ctrl+R
    app/views/staffs/index.html.erb

    練習：<table>を<table border="1">に変えてみましょう。

では、取引先企業(Company)を作ってみましょう。

.. code-block:: bash
    :linenos:

    % rails g scaffold Company name:string address1:string address2:string tel:string
    % rake db:migrate
    % rails s

次に、顧客をつくりましょう。
顧客(Customer)は取引先企業(Company)に所属しています。
そして、担当の社員(Staff)が一人います。

所属や担当などをデータベースでは **関係** と表現します。
リレーションと呼ばれます。この時、Railsでは「XXXXX_id」を生成することというルールがあります。


.. code-block:: bash
    :linenos:

    % rails g scaffold Customer name:string section:string company_id:integer staff_id:integer
    % rake db:migrate
    % rails s

http:// IPアドレス /customers/ にアクセスして下さい。
** 新規の登録は行わないで下さい！！！！ **

社員のIDや取引先企業のIDが解らないと登録できません。

改善してみましょう。
まずは、データベースの関係性をRails上で表現します。

.. code-block:: bash
    :linenos:

    % nano app/model/staff.rb

    class Staff < ActiveRecord::Base
      has_many :customers
    end

    Ctrl+O(保存) Enterで上書き保存。
    Ctrl+X(終了)


.. code-block:: bash
    :linenos:

    % nano app/model/company.rb

    class Company < ActiveRecord::Base
      has_many :customers
    end

    Ctrl+O Enter
    Ctrl+X


.. code-block:: bash
    :linenos:

    % nano app/model/customer.rb

    class Customer < ActiveRecord::Base
      belongs_to :company
      belongs_to :staff
    end


次に、入力フォームを修正します。

.. code-block:: bash
    :linenos:

    % nano app/view/customers/_form.html.erb

    <div class="field">
      <%= f.label :company_id %><br />
      <%= f.text_field :company_id %>
    </div>
    <div class="field">
      <%= f.label :staff_id %><br />
      <%= f.text_field :staff_id %>
    </div>


この部分を以下のようにする。

.. code-block:: bash
    :linenos:

    <div class="field">
      <%= f.label :company_id %><br />
      <%= f.collection_select :company_id, Company.all, :id, :name %>
    </div>
    <div class="field">
      <%= f.label :staff_id %><br />
      <%= f.collection_select :staff_id, Staff.all, :id, :name %>
    </div>

データベースに反映させ、サーバを起動する

.. code-block:: bash
    :linenos:

     % rake db:migrate
     % rails s

顧客の一覧表示を改善しましょう。


.. code-block:: bash
    :linenos:

    % nano app/view/customers/index

    <td><%= customer.company_id %></td>
    <td><%= customer.staff_id %></td>

    を以下のように変更する。

    <td><%= customer.company.name %></td>
    <td><%= customer.staff.name %></td>

    Ctrl+O Enter

メニューを作ってみましょう。


.. code-block:: bash
    :linenos:

    % rails n controller home index

    % nano app/views/home/index.html.erb

    以下を追記する。

    <li>
      <%= link_to "Company List", :controller => :companies, :action => :index %>
    </li>
    <li>
      <%= link_to "Customer List", :controller => :customers, :action => :index %>
    </li>
    <li>
      <%= link_to "Staff List", :controller => :staffs, :action => :index %>
    </li>

http:// IPアドレス /home/index へアクセスする。

ちょっと難しい連携を加えてみましょう。

.. code-block:: ruby
    :linenos:

    % nano config/route.rb

    resources :customers

    resources :companies do
      resources :customers
    end

    resources :staffs do
      resources :customers
    end

次にビューを修正します。

.. code-block:: bash
    :linenos:

    % nano app/views/companies/show.html.erb

    以下を加えます。

    <p>
     <b><%= link_to "customers", company_customers_path(@company) %></b>
    </p>

さらに、

.. code-block:: ruby
    :linenos:

    % nano app/controller/cusomers_controller.rb

    def index
      if params[:company_id].blank?
         @customers = Customer.all
      else
         @customers = Customer.where(:company_id => params[:company_id])
      end


のように修正します。
http:// IPアドレス:3000/companies/ にアクセスをして

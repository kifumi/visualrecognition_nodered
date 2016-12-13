# Watson Visual Recognition APIを使った画像認識アプリの作成

## 概要
IBM Watsonのサービスの一つであるVisual Recognition APIを呼びだす簡単なサンプルです。
Node-REDを使って簡単に呼び出しているのが特徴です。IBM Bluemixを使えば簡単に、迅速にアプリケーションを作ることが可能です。

## ノード解説 - visual recognition node
IBMがBluemixは様々なコグニティブAPIを提供しています。その中でも画像認識サービスである、Visual Recognition は画像解析から年齢や人物判定まで行う機能を持ったサービスです。IBM Watsonのカテゴリに入っているので確認してみてください。

## 全体フロー概要
画像のURL（例："http://xxxxx.jpg" ）をVisual Recognition のAPIにかけると画像解析を行い、顔認識の結果を返してくれるサンプルアプリです。
***
## 1. BluemixでNode-REDサービスを設定する
Bluemix Hands-On #1 の資料を参照してください。

## 2. Visual Recognition APIを追加する
Node-REDのノードに画像認識のための Visual Recognition があるのですが、このままでは使えません。 このNode-REDのアプリケーションにVisual Recognition APIを追加してあげる必要があります。
Bluemixのメニュー画面左上の「IBM Bluemix」をクリックし、「すべてのアプリ」一覧のなかから、先ほどのNode-REDのアプリケーションをクリックしてください。 

左側の「接続」をクリックし、右側の「新規に接続」のアイコンをクリックします。

左側の「Watson」をクリックし、「Visual Recognition」を選択します。
「作成」をクリックします。

「アプリケーションの再ステージ」のポップアップ画面が現れるので「再ステージ」をクリックします。

再ステージングし正常に再起動すればOKです！

## 3. Node-REDでプログラミング
「アプリの表示」をクリックし、「Go to your Node-RED flow editor」をクリックして、Node-REDがを起動します。

Node-REDエディターが立ち上がったら、上側右寄りの「＋」をクリックして、新しいフロー画面「Flow 2」を立ち上げます。

## 3-1. HTTP Input node


## 3-3. template node (初期画面)

    <h1>Welcome to a Watson Visual Recognition sample Face Detection app</h1>
    <H2>Recognize anyone?</H2>
    <form  action="{{req._parsedUrl.pathname}}">
    <img src="http://sysrun.haifa.il.ibm.com/ibm/history/exhibits/chairmen/images/watsonsr.jpg" height='200'/> 
    <img src="http://www.awaken.com/wp-content/uploads/2015/05/forbes.jpg" height='200'/>  
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/LinuxCon_Europe_Linus_Torvalds_03.jpg/220px-LinuxCon_Europe_Linus_Torvalds_03.jpg" height='200'/>   
    <img src="http://smashinghub.com/wp-content/uploads/2012/01/nb5.jpg" height='200'/>     
    <br/>Right-click one of the above images and select Copy image location and paste the URL in the box below.<br>Do an image search for faces, try multiple faces. After you click on an image, to the right it usually says "View image" click that to get the URL.<br/>
    <br>Image URL: <input type="text" name="imageurl"/>   
    <input type="submit" value="Analyze"/>
    </form>
    
## 3-6. template node (結果)

        <h1>Visual Recognition v3 Image Analysis</h1>    
        <p>Analyzed image: {{result.images.0.resolved_url}}<br/><img id="image” 
        src="{{result.images.0.resolved_url}}" height="200"/></p>    
        {{^result}}        
        <P>No Face detected</P>    
        {{/result}}    
        <p>Images Processed: {{result.images_processed}}</p>    
        <table border='1'>        
        <thead><tr><th>Age Range</th><th>Confidence</th><th>Gender</th><th>Confidence</th><th>Name</th></tr></thead>        
        {{#result.images.0.faces}}<tr>            
        <td><b>{{age.min}} - {{age.max}}</b></td><td><i>{{age.score}}</i></td>            <td>{{gender.gender}}</td>
        <td>{{gender.score}}</td>            <td>{{identity.name}} ({{identity.score}})</td>       
        </tr>{{/result.images.0.faces}}    
        </table>    
        <form  action="{{req._parsedUrl.pathname}}">        
        <br><input type="submit" value="Try again or go back to the home page"/>    
        </form>

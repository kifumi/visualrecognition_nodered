# visualrecognition_nodered
Node-REDでVisual Recognition APIを使って顔を認識するアプリ
==========
3-3のコード
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
==========
3-6のコード
<h1>Visual Recognition v3 Image Analysis</h1>
    <p>Analyzed image: {{result.images.0.resolved_url}}<br/><img id="image" src="{{result.images.0.resolved_url}}" height="200"/></p>
    {{^result}}
        <P>No Face detected</P>
    {{/result}}
    <p>Images Processed: {{result.images_processed}}</p>
    <table border='1'>
        <thead><tr><th>Age Range</th><th>Confidence</th><th>Gender</th><th>Confidence</th><th>Name</th></tr></thead>
        {{#result.images.0.faces}}<tr>
            <td><b>{{age.min}} - {{age.max}}</b></td><td><i>{{age.score}}</i></td>
            <td>{{gender.gender}}</td><td>{{gender.score}}</td>
            <td>{{identity.name}} ({{identity.score}})</td>
        </tr>{{/result.images.0.faces}}
    </table>
    <form  action="{{req._parsedUrl.pathname}}">
        <br><input type="submit" value="Try again or go back to the home page"/>
    </form>

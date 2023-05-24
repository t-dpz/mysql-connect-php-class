<h3>Connect to MySQL database:</h3>
<pre><code class="lang-php">include &#039;db.php&#039;;

$dbhost = &#039;localhost&#039;;
$dbuser = &#039;root&#039;;
$dbpass = &#039;&#039;;
$dbname = &#039;example&#039;;

$db = new db($dbhost, $dbuser, $dbpass, $dbname);</code></pre>
<br>
<h3>Fetch a record from a database:</h3>
<pre><code class="lang-php">$account = $db-&gt;query(&#039;SELECT * FROM accounts WHERE username = ? AND password = ?&#039;, &#039;test&#039;, &#039;test&#039;)-&gt;fetchArray();
echo $account[&#039;name&#039;];</code></pre>
<p>Or you could do:</p>
<pre><code class="lang-php">$account = $db-&gt;query(&#039;SELECT * FROM accounts WHERE username = ? AND password = ?&#039;, array(&#039;test&#039;, &#039;test&#039;))-&gt;fetchArray();
echo $account[&#039;name&#039;];</code></pre>
<br>
<h3>Fetch multiple records from a database:</h3>
<pre><code class="lang-php">$accounts = $db-&gt;query(&#039;SELECT * FROM accounts&#039;)-&gt;fetchAll();

foreach ($accounts as $account) {
	echo $account[&#039;name&#039;] . &#039;&lt;br&gt;&#039;;
}</code></pre>
<p>You can specify a callback if you do not want the results being stored in an array (useful for large amounts of data):</p>
<pre><code class="language-php">$db-&gt;query(&#039;SELECT * FROM accounts&#039;)-&gt;fetchAll(function($account) {
    echo $account[&#039;name&#039;];
});</code></pre>
<p>If you need to break the loop you can add:</p>
<pre><code class="language-php">return &#039;break&#039;; </code></pre>
<h3>Get the number of rows:</h3>
<pre><code class="lang-php">$accounts = $db-&gt;query(&#039;SELECT * FROM accounts&#039;);
echo $accounts-&gt;numRows();</code></pre>
<br>
<h3>Get the affected number of rows:</h3>
<pre><code class="lang-php">$insert = $db-&gt;query(&#039;INSERT INTO accounts (username,password,email,name) VALUES (?,?,?,?)&#039;, &#039;test&#039;, &#039;test&#039;, &#039;test@gmail.com&#039;, &#039;Test&#039;);
echo $insert-&gt;affectedRows();</code></pre>
<br>
<h3>Get the total number of queries:</h3>
<pre><code class="lang-php">echo $db-&gt;query_count;</code></pre>
<br>
<h3>Get the last insert ID:</h3>
<pre><code class="lang-php">echo $db-&gt;lastInsertID();</code></pre>
<br>
<h3>Close the database:</h3>
<pre><code class="lang-php">$db-&gt;close();</code></pre>

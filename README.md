

<figure class="wp-block-image"><img decoding="async" src="./img_files/visual-selection01-1024x707.png" alt="An attempt to predict the behavior of the properties of the secp256k1 Elliptic Curve: Cryptography and cryptocurrency related parameters secp256k1 reveals several vulnerabilities and potential threats:" class="wp-image-1698"></figure>



<ol class="wp-block-list">
<li><a href="https://cryptodeeptech.ru/twist-attack" target="_blank" rel="noreferrer noopener"><strong>Elliptic Curve Point Compression Vulnerability</strong>&nbsp;:</a>
<ul class="wp-block-list">
<li>In 2017, a vulnerability was discovered in the&nbsp;<strong>secp256k1</strong>&nbsp;library related to elliptic curve point compression. The compression algorithm could return an incorrect compressed representation of a point under certain conditions, which could lead to loss of funds or data integrity in cryptocurrency projects&nbsp;<a href="https://cryptodeeptech.ru/twist-attack" target="_blank" rel="noreferrer noopener">1</a>&nbsp;.</li>



<li>This vulnerability has been fixed in an updated version of the library.</li>
</ul>
</li>



<li><a href="https://cryptodeeptech.ru/quantum-attacks-on-bitcoin/" target="_blank" rel="noreferrer noopener"><strong>Quantum attacks</strong>&nbsp;:</a>
<ul class="wp-block-list">
<li>Quantum computers could potentially break elliptic curve cryptographic systems, including&nbsp;<strong>secp256k1</strong>&nbsp;, using Shor’s algorithm. This could lead to the compromise of digital signatures and access to private keys&nbsp;<a href="https://cryptodeeptech.ru/quantum-attacks-on-bitcoin/" target="_blank" rel="noreferrer noopener">2</a>&nbsp;.</li>



<li>Researchers predict that quantum computers could crack Bitcoin by 2027 unless steps are taken to transition to post-quantum cryptographic schemes&nbsp;<a href="https://cryptodeeptech.ru/quantum-attacks-on-bitcoin/" target="_blank" rel="noreferrer noopener">2</a>&nbsp;.</li>
</ul>
</li>



<li><a href="https://cryptodeeptech.ru/signature-malleability" target="_blank" rel="noreferrer noopener"><strong>Signature Malleability Vulnerability</strong>&nbsp;:</a>
<ul class="wp-block-list">
<li>While not directly related to the&nbsp;<strong>secp256k1</strong>&nbsp;parameters , but affecting ECDSA, which is used in Bitcoin, the Signature Malleability vulnerability allows attackers to change signatures without invalidating them. This can be used for a variety of attacks, including transaction forgery&nbsp;<a href="https://cryptodeeptech.ru/signature-malleability" target="_blank" rel="noreferrer noopener">4</a>&nbsp;.</li>
</ul>
</li>



<li><strong><a href="https://cryptodeeptech.ru/jacobian-curve-algorithm-vulnerability" target="_blank" rel="noreferrer noopener">Jacobian Curve algorithm vulnerability:</a></strong>
<ul class="wp-block-list">
<li>This vulnerability involves manipulating the mathematical properties of the Jacobi coordinates used in ECDSA. It allows forgeries to be created with valid signatures, potentially breaking consensus on the Bitcoin&nbsp;<a href="https://cryptodeeptech.ru/jacobian-curve-algorithm-vulnerability" target="_blank" rel="noreferrer noopener">5</a>&nbsp;network .</li>
</ul>
</li>



<li><a href="https://cryptodeeptech.ru/discrete-logarithm" target="_blank" rel="noreferrer noopener"><strong>Using AI to analyze patterns</strong>&nbsp;:</a>
<ul class="wp-block-list">
<li>Research has shown that simple neural networks can detect patterns in the sequence of points on the&nbsp;<strong>secp256k1</strong>&nbsp;curve , which could potentially be used for future attacks&nbsp;<a href="https://cryptodeeptech.ru/discrete-logarithm" target="_blank" rel="noreferrer noopener">6</a>&nbsp;.</li>
</ul>
</li>
</ol>



<hr class="wp-block-separator has-alpha-channel-opacity">



<!-- wp:heading -->
<h2 class="wp-block-heading">On some properties of the secp256k1 curve and an attempt to predict its behavior.</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>As is well known, the discrete logarithm problem is very difficult and people do not know how to calculate it quickly. Moreover, knowing a point on the curve P = n*G, it is very difficult to make a judgment about the value of n. Even about an approximate value. Let's try something even simpler: let's try to make judgments about the sequence&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://habrastorage.org/getpro/habr/formulas/7fa/5d7/b73/7fa5d7b733684aea1f89409e0d3e35eb.svg" alt="$P(i) = i*G$"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>, or rather about the meanings&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://habrastorage.org/getpro/habr/formulas/bf8/3b5/32c/bf83b532cd867d34004f8eded8c5c79a.svg" alt="$i$"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>&nbsp;knowing the meanings&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://habrastorage.org/getpro/habr/formulas/521/014/00d/52101400d2897f247fb0a4389ac066c7.svg" alt="$P(i)$"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>.<br><a target="_blank" rel="noreferrer noopener"></a><br>Let's try to determine how much this sequence differs from a random sequence. If the sequence&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://habrastorage.org/getpro/habr/formulas/521/014/00d/52101400d2897f247fb0a4389ac066c7.svg" alt="$P(i)$"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>&nbsp;complex and difficult to predict, it will not differ from a random sequence. And if it does differ, it means that the sequence of points of the secp256k1 curve is not so complex.<br>Let's build a neural network that we will train on the training sequence to distinguish sequences.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>If we can distinguish between a random sequence and a sequence of points, then this will mean that there is some algorithm that can be computed quickly enough to make judgments about the logarithm.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Let me remind you that calculating the discrete logarithm on an elliptic curve is a very difficult task.<br>Let us take a pre-calculated random sequence for repeatability of the experiment. The quality of this sequence can be checked</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>dieharder -f PM_rand_600.bin -g 201 -a</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>You can also check nist, but the result will be almost the same.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Let's create a program that will mix the y coordinate of the curve point sequence and a random sequence in a ratio of 1:8 and write it to the file x600_btc_32_LH.bin and simultaneously write a pointer to the source - curve or random - to y600_btc_32_LH.bin.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>data_preparation.cpp</strong></p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include &lt;iostream&gt;<br>#include &lt;stdlib.h&gt;<br>#include &lt;stdio.h&gt;<br>#include &lt;openssl/bn.h&gt;<br>#include &lt;openssl/ec.h&gt;<br>#include &lt;openssl/err.h&gt;<br>#include &lt;openssl/symhacks.h&gt;<br><br><strong>using</strong> <strong>namespace</strong> std;<br><br><strong>int</strong> main() {<br>	<strong>int</strong> bits = 256;<br><br>	<strong>unsigned</strong> <strong>char</strong> buf&#91;32];<br><br>	<strong>char</strong> <strong>*</strong>pr;<br><br>	EC_GROUP *group;<br>	EC_KEY *eckey = EC_KEY_new();<br>	EC_POINT *P;<br><br>	BN_CTX *ctx = BN_CTX_new();<br>	BIGNUM *x = BN_new();<br>	BIGNUM *n = BN_new();  // начало последовательности точек кривой<br>	BIGNUM *y = BN_new();<br><br>	<strong>char</strong> e_buf&#91;256];<br><br>	FILE * xFile;<br>	FILE * yFile;<br>	FILE * rFile;<br>	xFile = fopen("x600_btc_32_LH.bin", "wb");<br>	yFile = fopen("y600_btc_32_LH.bin", "wb");<br><br>	rFile = fopen("PM_rand_600_t.bin", "rb");<br>	<strong>if</strong> (rFile==NULL)<br>	{ cout&lt;&lt;" PM_rand.bin NOT FOUND"; <strong>return</strong> -1; }<br><br>	srand(time(NULL));<br>// nid 714. curve secp256k1<br>	<strong>int</strong> nid = 714;<br>	<strong>if</strong> ((group = EC_GROUP_new_by_curve_name(nid)) == NULL) {<br>		fprintf(stdout, "\nEC_GROUP_new_curve_name() failed with"<br>				" curve %s\n  nid %x", nid);<br>	}<br>	<strong>if</strong> (eckey == NULL) {<br>		cout &lt;&lt; "ABORT2 ";<br>		ERR_error_string(ERR_get_error(), e_buf);<br>		cout &lt;&lt; "E_BUF " &lt;&lt; e_buf &lt;&lt; endl;<br>	}<br><br>	<strong>if</strong> (!EC_KEY_set_group(eckey, group)) {<br>		cout &lt;&lt; "ABORT3 ";<br>		ERR_error_string(ERR_get_error(), e_buf);<br>		cout &lt;&lt; "E_BUF " &lt;&lt; e_buf &lt;&lt; endl;<br>	}<br><br>	EC_GROUP_precompute_mult(group, ctx);<br><br><br>	P = EC_POINT_new(group);<br><br>	BN_rand(n, bits, BN_RAND_TOP_ONE, BN_RAND_BOTTOM_ANY);<br>	// n - начало выборки<br>	<strong>int</strong> NN = 60000;<br><br>	<strong>for</strong> (<strong>int</strong> i = 0; i &lt; NN; i++) {<br><br>		<strong>if</strong> ((rand() % 128) &lt; 16) {<br>			pr = (<strong>char</strong> <strong>*</strong>) "1";<br><br>			<strong>if</strong> (!EC_POINT_mul(group, P, n, NULL, NULL, ctx)) {<br>				cout &lt;&lt; "ABORT_10 ";<br>				ERR_error_string(ERR_get_error(), e_buf);<br>				cout &lt;&lt; "E_BUF " &lt;&lt; e_buf &lt;&lt; endl;<br>			}<br>			<strong>if</strong> (!EC_POINT_get_affine_coordinates_GFp(group, P, x, y, ctx)) {<br>				cout &lt;&lt; "ABORT_11 ";<br>				ERR_error_string(ERR_get_error(), e_buf);<br>				cout &lt;&lt; "E_BUF " &lt;&lt; e_buf &lt;&lt; endl;<br>			}<br>			BN_bn2bin(y, buf);<br>		} <strong>else</strong> {<br>			pr = (<strong>char</strong> <strong>*</strong>) "0";<br>			<strong>int</strong> cind = fread(buf, 32, 1, rFile); // read 32 byte = 256 bit<br>		}<br>		fwrite(buf, 32, 1, xFile);<br>		BN_add_word(n, 1L);  // in P new point n+i<br>		fwrite(pr, 1, 1, yFile);<br><br>	}<br><br>	fclose(xFile);<br>	fclose (yFile);<br><br>	BN_CTX_free(ctx);<br>	EC_GROUP_free(group);<br>	BN_free(x);<br>	BN_free(y);<br><br>}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>And we will feed the two received files x600_btc_32_LH.bin and y600_btc_32_LH.bin to the network.</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code><strong>from</strong> keras.models <strong>import</strong> Model<br><strong>from</strong> keras.utils <strong>import</strong> np_utils<br><strong>from</strong> keras.layers <strong>import</strong> Dense, Input<br><strong>from</strong> keras.layers <strong>import</strong> Bidirectional, GRU<br><strong>from</strong> keras.models <strong>import</strong> Model<br><strong>from</strong> keras.optimizers <strong>import</strong> RMSprop<br><br><br><strong>import</strong> numpy <strong>as</strong> np<br><strong>import</strong> keras <strong>as</strong> ks<br><br>num_classes = 2 <br><br>length = 32<br>length_8 = length&lt;&lt;3<br>num_train = 50000<br>num_test = 10000<br><br><br>X_train = np.zeros(shape=(num_train, length_8), dtype='uint8')<br>y_train = np.zeros(shape=(num_train), dtype='uint8')<br><br>X_test = np.zeros(shape=(num_test, length_8), dtype='uint8')<br>y_test = np.zeros(shape=(num_test), dtype='uint8')<br><br>bx_train = np.zeros(shape=(num_train, length), dtype='uint8')<br>bx_test = np.zeros(shape=(num_test, length), dtype='uint8')<br><br>f_x = open("./input/x600_btc_32_LH.bin", 'rb')<br><strong>for</strong> k <strong>in</strong> xrange(num_train):<br>    <strong>for</strong> i <strong>in</strong> xrange(32):<br>        bx_train&#91;k, i] = ord(f_x.read(1))<br><br><strong>for</strong> k <strong>in</strong> xrange(num_test):<br>    <strong>for</strong> i <strong>in</strong> xrange(32):<br>        bx_test&#91;k, i] = ord(f_x.read(1))<br><br>f_x.close()<br><br>f_y = open("./input/y600_btc_32_LH.bin", 'rb')<br><strong>for</strong> i <strong>in</strong> xrange(num_train):<br>    y_train&#91;i] = ord(f_y.read(1))<br><br><strong>for</strong> i <strong>in</strong> xrange(num_test):<br>    y_test&#91;i] = ord(f_y.read(1))<br>    <br>f_y.close()<br>y_train -= 48<br>y_test -= 48</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>Let's convert it to a bit-to-byte format. That is, we transfer one bit of the original sequence to a byte.</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>tab = np.zeros((256,8),dtype='int8')<br><strong>for</strong> i <strong>in</strong> xrange(256):<br>    mask = 1<br>    <strong>for</strong> j <strong>in</strong> xrange(8):<br>        <strong>if</strong> i &amp; mask == 0:<br>            tab&#91;i,j] = 0<br>        <strong>else</strong>:<br>            tab&#91;i,j] = 1<br>        mask&lt;&lt;1<br><strong>for</strong> k <strong>in</strong> xrange(num_train):<br>    <strong>for</strong> i <strong>in</strong> xrange(length):<br>        <strong>for</strong> j <strong>in</strong> xrange(8):<br>            X_train&#91;k,i*8+j] = tab&#91;bx_train&#91;k,i],j]<br>            <br><strong>for</strong> k <strong>in</strong> xrange(num_test):<br>    <strong>for</strong> i <strong>in</strong> xrange(length):<br>        <strong>for</strong> j <strong>in</strong> xrange(8):<br>            X_test&#91;k,i*8+j] = tab&#91;bx_test&#91;k,i],j]</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>Let's convert it to float format and scale it to 0.004 and prepare Y.</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>X_train = X_train.astype('float32') <br>X_test = X_test.astype('float32')<br>X_train /= 255.<br>X_test /= 255.<br><br>Y_train = np_utils.to_categorical(y_train, num_classes)<br>Y_test = np_utils.to_categorical(y_test, num_classes)</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>We will take a fairly simple network, only slightly changing the activation function.</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code><strong>import</strong> math<br><strong>from</strong> keras <strong>import</strong> backend <strong>as</strong> K<br><strong>from</strong> keras.utils.generic_utils <strong>import</strong> get_custom_objects<br><strong>from</strong> keras.layers <strong>import</strong> Activation<br><br><strong>def</strong> gaussian(x):<br>    mu = 64.<br>    sigma = 10.<br>    xx = -0.5*((x-mu)/sigma)**2 / sigma / math.sqrt(2*math.pi)<br>    <strong>return</strong> K.exp(xx)<br><br>get_custom_objects().update({'gaussian': Activation(gaussian)})<br><br>batch_size = 32<br>num_epochs = 16<br>hidden_size_1 = 1024<br>hidden_size_2 = 1024<br><br>X_train = X_train.reshape(num_train,16,16)<br>X_test = X_test.reshape(num_test,16,16)<br><br>inp = Input(shape=(16,16,))<br>x = Bidirectional(GRU(1024, return_sequences=<strong>True</strong>))(inp)<br>x = Bidirectional(GRU(1024, return_sequences=<strong>False</strong>))(x)<br>x = Dense(hidden_size_1, activation='sigmoid')(x)<br>x = Dense(hidden_size_2, activation='gaussian')(x)<br><br>out = Dense(num_classes, activation='gaussian')(x) <br><br>model = Model(inputs=inp, outputs=out)<br>model.compile(loss='binary_crossentropy',<br>#              optimizer='adam',<br>              optimizer=RMSprop(lr=0.0001,clipvalue=1, clipnorm=1),<br>              metrics=&#91;'accuracy'])</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>The result is quite acceptable, the network distinguishes a sequence of curve points from a random sequence, not as accurately as we would like, but it makes a judgment about the logarithm.</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>mod = model.fit(X_train, Y_train, # Train the model using the training set...<br>          batch_size=batch_size, epochs=2,<br>          verbose=1, validation_data=(X_test, Y_test))<br><br>Train on 50000 samples, validate on 10000 samples<br>Epoch 1/2<br>val_loss: 0.3706 - val_acc: 0.8783<br>Epoch 2/2<br>val_loss: 0.3703 - val_acc: 0.8783</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>We found that a simple regular neural network can distinguish between a random sequence and a sequence of secp256k1 curve points. This suggests that the network is detecting patterns in a sequence that must be very complex.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>As of today, this is the most serious vulnerability of the secp256k1 curve and sooner or later the victory will be for AI.</p>
<!-- /wp:paragraph -->



<hr class="wp-block-separator has-alpha-channel-opacity">



<p>This material was created for the&nbsp;&nbsp;&nbsp;<a href="https://cryptodeep.ru/" target="_blank" rel="noreferrer noopener">CRYPTO DEEP TECH</a>&nbsp;&nbsp;portal to ensure financial data security and cryptography on elliptic curves&nbsp;&nbsp;&nbsp;<a href="https://www.youtube.com/@cryptodeeptech" target="_blank" rel="noreferrer noopener">secp256k1</a>&nbsp;&nbsp;&nbsp;against weak&nbsp;&nbsp;&nbsp;<a href="https://github.com/demining/CryptoDeepTools" target="_blank" rel="noreferrer noopener">ECDSA</a>&nbsp;&nbsp;signatures in the&nbsp;&nbsp;&nbsp;<a href="https://t.me/cryptodeeptech" target="_blank" rel="noreferrer noopener">BITCOIN</a>&nbsp;&nbsp;cryptocurrency. The creators of the software are not responsible for the use of materials.</p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p><strong><a href="https://github.com/demining/An-attempt-to-predict-the-behavior-of-the-properties-of-the-secp256k1-Elliptic-Curve" target="_blank" rel="noreferrer noopener">Source code</a></strong></p>



<p><strong><a href="https://colab.research.google.com/drive/1jqHX5Oawy3QPh2OSYVf6AF1RGtjAb4rj?usp=sharing" target="_blank" rel="noreferrer noopener">Google Colab</a></strong></p>



<p><strong><a href="https://bitcoinchatgpt.org/" target="_blank" rel="noreferrer noopener">BitcoinChatGPT</a></strong></p>



<p><strong><a href="https://dustattack.org/blockchain-folbit-leaks" target="_blank" rel="noreferrer noopener">Blockchain Folbit Leaks</a></strong></p>



<p><strong><a href="https://dockeyhunt.com/dockeyhunt-deep-learning" target="_blank" rel="noreferrer noopener">Dockeyhunt Deep Learning</a></strong></p>



<p><strong><a href="https://t.me/cryptodeeptech" target="_blank" rel="noreferrer noopener">Telegram: https://t.me/cryptodeeptech</a></strong></p>



<p><strong><a href="https://youtu.be/p62orC7WDUE" target="_blank" rel="noreferrer noopener">Video material: https://youtu.be/p62orC7WDUE</a></strong></p>



<p><strong><a href="https://dzen.ru/video/watch/67c3e91abbfa683a745a0aea" target="_blank" rel="noreferrer noopener">Video tutorial: https://dzen.ru/video/watch/67c3e91abbfa683a745a0aea</a></strong></p>



<p><strong><a href="https://cryptodeeptech.ru/quantum-attacks-on-bitcoin" target="_blank" rel="noreferrer noopener">Source: https://cryptodeeptech.ru/quantum-attacks-on-bitcoin</a></strong></p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./img_files/visual-selection01-1024x707.png" alt="An attempt to predict the behavior of the properties of the secp256k1 Elliptic Curve: Cryptography and cryptocurrency related parameters secp256k1 reveals several vulnerabilities and potential threats:" class="wp-image-1698"></figure>
                                </div>
</article>
  

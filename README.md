<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ads Test Page</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    background:#000000;
    color:#ffffff;
    min-height:100vh;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    padding-bottom:120px;
    font-family:Segoe UI, sans-serif;
}

h1{
    margin-bottom:20px;
}

.banner-container{
    position:fixed;
    bottom:0;
    left:0;
    width:100%;
    display:flex;
    justify-content:center;
    align-items:center;
    min-height:90px;
    background:rgba(0,0,0,0.7);
    z-index:9999;
}
</style>

</head>
<body>

<h1>Banner & Social Bar Test</h1>
<p>If everything works, you should see both ads.</p>

<!-- Banner Ad -->
<div class="banner-container">

<script>
atOptions = {
    'key' : '0060a66942efa379761d703d1b4b8a14',
    'format' : 'iframe',
    'height' : 90,
    'width' : 728,
    'params' : {}
};
</script>

<script src="https://www.highperformanceformat.com/0060a66942efa379761d703d1b4b8a14/invoke.js"></script>


</div>

<!-- Social Bar -->
<script src="https://pl29659533.effectivecpmnetwork.com/66/5a/20/665a203e5d7e2ff6ed7a6d50be88fe86.js"></script>

</body>
</html>

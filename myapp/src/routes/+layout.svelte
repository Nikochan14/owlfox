<script>

    import ts from "typescript";

</script>
<div id="site-background" style="background-color: hsla({Math.random() * 360}, 100%, 100%, 1);">
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container-fluid">
            <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
            <div class="navbar-nav mx-auto">
                <a class="nav-link" href="/dance">Dance?</a>
                <a class="nav-link" aria-current="page" href="/">Home</a>
                <a class="nav-link" href="/">Bureaucracy</a>
                <a class="nav-link" href="/">Differential Equations</a>
                <a class="nav-link"  href="/"aria-disabled="true">Gaming</a>
            </div>
            </div>
        </div>
    </nav>

    <div class="container content-baby">
        <slot />
    </div>
</div>

<style>
    #site-background {
        /* background-image: url("https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fstatic1.thethingsimages.com%2Fwordpress%2Fwp-content%2Fuploads%2F2018%2F01%2Ffox-vs-owl.jpg&f=1&nofb=1&ipt=49e0512dc780a7c66bbf81f82e3a06d96c47d65295a89c3a7d2d035aaf146961&ipo=images"); */
        background-size: 100vw;
        background-repeat: no-repeat;
        width: 100vw;
        height: 100vh;
        z-index: 1;
    }
</style>

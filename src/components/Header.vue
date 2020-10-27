<template>
    <div>
        <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
            <a class="navbar-brand" href="#"><b>Fancy Quiz Application</b></a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                
                
                </ul>
            </div>
        </nav>
        <center><b class="navy">Correct: {{numCorrect}}/{{numTotal}} :Total</b></center>
    </div>
</template>

<script>
export default {
    name: 'Header',
    props: ['numCorrect', 'numTotal']
}
</script>

<style scoped>
    .navy {
        font-family: monospace;
        font-size: 1.8rem;
    }
</style>
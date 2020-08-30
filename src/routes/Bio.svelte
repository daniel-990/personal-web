<script>
    import axios from "axios";
    import { onMount } from "svelte";
    
    const datosBlog = {
        "datos":"https://server-personal.herokuapp.com/json-blog.php"
    };

        // Make a request for a user with a given ID
    axios.get(datosBlog.datos)
    .then(function (response) {
        console.log(response.data);
    })
    .catch(function (error) {
        console.log(error);
    })
    .then(function () {
        // always executed
    });

</script>

<div class="conteiner">
    <h1>
        
    </h1>
</div>
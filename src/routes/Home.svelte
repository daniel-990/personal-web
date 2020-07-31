<script>
    import axios from "axios";
    import { onMount } from "svelte";

	const datos = {
		"img":"img/back.png",
        "datosIn":"http://localhost:5000/data/data.json"
	}

	let datosInst;
	let titulo;
	let nombre;
	let fotoPerfil;
    let perfil;
    let imagenes = [];

    // Make a request for a user with a given ID
    axios.get(datos.datosIn)
    .then(function (response) {

        nombre = response.data.graphql.user.full_name;
        titulo = response.data.graphql.user.biography;
        perfil = response.data.graphql.user.username;
        fotoPerfil = response.data.graphql.user.profile_pic_url;
        imagenes = response.data.graphql.user.edge_owner_to_timeline_media.edges;

        console.log(imagenes);
        
    })
    .catch(function (error) {
        console.log(error);
    })
    .then(function () {
        // always executed
    });
</script>

    <section class="banner" style="background-image: url('{datos.img}');"></section>
	<section class="contenedor-cabecera">
        <div class="container">
            <!-- <img src="{datos.img}" class="img-fluid" alt=""> -->
            <hr>
            <div class="media">
            <img class="mr-3 align-self-start" src="{fotoPerfil}" alt="foto de perfil {nombre}e">
                <div class="media-body">
                    <h5 class="mt-0">{nombre}</h5>
                    {titulo}
                    <br>
                    <a href="http://instagram.com/{perfil}" target="blanc_"><i class="fab fa-instagram"></i> - @{perfil}</a>
                </div>
            </div>
            <hr>
            <div class="row fondo">
                {#each imagenes as img}
                    <div class="col-md-4 espacio">
                        <img class="img_ img-responsive borde" title="{img.node.accessibility_caption}" alt="{img.node.accessibility_caption}" src="{img.node.display_url}">
                        <!-- <small class="autor">Autor: {nombre}</small> -->
                    </div>
                {/each}
            </div>
        </div>
	</section>


<style>
    .banner{
        width: 100%;
        height: 500px;
        background-position: center;
        background-size: cover;
        background-attachment: fixed;
        background-repeat: no-repeat;
    }
	.contenedor-cabecera{
        padding: 30px;
	}
	a{
		text-decoration: none !important;
		color:blueviolet;
	}
    .img_{
        width: 100%;
    }
    .borde{
        border: 5px solid black;
    }
    .espacio{
        padding: 10px;
    }
    .autor{
        position: relative;
        top: -29px;
        color: black;
        left: 8px;
    }
</style>
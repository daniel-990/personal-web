<script>
    import axios from "axios";
    import { onMount } from "svelte";

	const datos = {
		"img":"img/back.png",
        "datosInstagram":"https://www.instagram.com/daniel.arango.villegas/?__a=1"
    }

	let datosInst;
	let titulo;
	let nombre;
	let fotoPerfil;
    let perfil;
    let imagenes = [];

    // Make a request for a user with a given ID
    axios.get(datos.datosInstagram)
    .then(function (response) {
        nombre = response.data.graphql.user.full_name;
        titulo = response.data.graphql.user.biography;
        perfil = response.data.graphql.user.username;
        fotoPerfil = response.data.graphql.user.profile_pic_url;
        imagenes = response.data.graphql.user.edge_owner_to_timeline_media.edges;
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
                    <a href="http://instagram.com/{perfil}" class="boton-link" target="blanc_"><i class="fab fa-instagram icono"></i> - @{perfil}</a>
                </div>
            </div>
            <hr>
            <div class="row fondo">
                {#each imagenes as img}
                    <div class="col-md-4 espacio">
                        <a href="{img.node.display_url}" target="blank_">
                            <img class="img_ img-responsive borde" title="{img.node.accessibility_caption}" alt="{img.node.accessibility_caption}" src="{img.node.display_url}">
                        </a>
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
        color: #9E9E9E;
        font-weight: 700;
	}
    a:hover{
		text-decoration: none !important;
        color: #9E9E9E;
        font-weight: 700;
	}
    .icono{
        background: radial-gradient(circle at 30% 107%, #fdf497 0%, #fdf497 5%, #fd5949 45%, #d6249f 60%, #285AEB 90%);
        -webkit-background-clip: text;
        background-clip: text;
        -webkit-text-fill-color: transparent;
        font-size: 20px;
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
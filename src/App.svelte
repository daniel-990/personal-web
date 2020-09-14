<script>
    import axios from "axios";
	import { onMount } from "svelte";
	
	/*

	const datosBlog = {
        "datos":"https://server-personal.herokuapp.com/json-blog.php"
    };

    let contenido = [];
    
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
	
	*/

	const datos = {
		"img":"img/back.png",
        "datosInstagram":"https://www.instagram.com/daniel.arango.villegas/?__a=1",
        "datosWeb":"https://server-personal.herokuapp.com/json-blog.php"
    }

	let datosInst;
	let titulo;
	let nombre;
	let fotoPerfil;
    let perfil;
    let imagenes = [];
    let contenido = [];

    // datos de instagram
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
    //datos del portafolio
    axios.get(datos.datosWeb)
        .then(function (response) {
            console.log(response.data);
            contenido = response.data;
        })
        .catch(function(error) {
            console.log(error);
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
    <section class="contenedor-datos-portafolio">
        <div class="container">
            <h1>☕ | 2020</h1>
            <br>
            <div class="contenido">
                {#each contenido as contenidosPortfolio}
                    <div class="card">
                        <div class="card-body">
                            <h5 class="card-title">
                                {contenidosPortfolio.titulo}
                            </h5>
                            <p class="card-text">{contenidosPortfolio.contenido}</p>
                            <a href="{contenidosPortfolio.subtitulo}">Mas información</a>
                            <hr>
                            <span class="badge badge-danger">{contenidosPortfolio.fecha}</span>
                        </div>
                    </div>
                    <br>
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
    .card{
        color:black;
    }
</style>
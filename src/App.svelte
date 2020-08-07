<script>
	import { Router, Route } from "svelte-routing";
  	import NavLink from "./components/NavLink.svelte";

	//importamos las rutas
	import Biografia from "./routes/Bio.svelte";
	import Home from "./routes/Home.svelte";

	export let url = "";
	
</script>

<Router url="{url}">
		<nav class="menu-principal navbar navbar-expand-lg navbar-dark bg-dark">
			<a class="navbar-brand" href="/"><i class="fas fa-ghost"></i></a>
			<button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
			<span class="navbar-toggler-icon"></span>
			</button>
			<div class="collapse navbar-collapse" id="navbarNavAltMarkup">
			<div class="navbar-nav">
				<a class="nav-item nav-link" href="#"><NavLink to="/">Home</NavLink></a>
				<a class="nav-item nav-link" href="#"><NavLink to="biografia">Biografia</NavLink></a>
			</div>
			</div>
		</nav>
		<div>
		<Route path="/" component="{Home}" />
		<Route path="biografia" component="{Biografia}" />
	</div>
</Router>

<style>
	a{
		color: white !important;
	}
</style>

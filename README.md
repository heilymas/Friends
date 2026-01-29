<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Hevemh Hogar - Catálogo Interactivo</title>
  <meta name="description" content="Catálogo de muebles y artículos para el hogar — Hevemh Hogar. Pide por WhatsApp.">
  <style>
    body { font-family: 'Segoe UI', sans-serif; margin: 0; background-color: #f8f9fa; color: #333; }
    header { background-color: #2c3e50; color: white; padding: 2rem 1rem; text-align: center; position: sticky; top: 0; z-index: 1000; }
    .contenedor-busqueda { margin-top: 15px; }
    #buscador { padding: 12px; width: 80%; max-width: 400px; border-radius: 25px; border: none; outline: none; font-size: 1rem; }
    .catalogo { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 25px; padding: 40px 20px; max-width: 1200px; margin: auto; }
    .producto { background: white; border-radius: 15px; padding: 20px; box-shadow: 0 5px 15px rgba(0,0,0,0.08); text-align: center; transition: 0.3s; }
    .oculto { display: none; }
    .producto img { width: 100%; height: 200px; object-fit: cover; border-radius: 10px; }
    .precio { color: #27ae60; font-size: 1.4rem; font-weight: bold; margin: 15px 0; }
    .btn-whatsapp { background-color: #25d366; color: white; text-decoration: none; padding: 10px 20px; border-radius: 8px; font-weight: bold; border: none; cursor: pointer; width: 100%; }
    .btn-whatsapp:hover { background-color: #128c7e; }
  </style>
</head>
<body>
<header>
    <h1>HEVEMH HOGAR</h1>
    <div class="contenedor-busqueda">
        <input id="buscador" type="search" aria-label="Buscar productos" placeholder="🔍 Buscar muebles, lámparas...">
    </div>
</header>

<section class="catalogo" id="lista-productos" role="list" aria-live="polite">
    <div class="producto" role="listitem" data-nombre="Sofá Moderno Gris" data-descripcion="Tela suave y estructura reforzada" data-precio="450">
        <img loading="lazy" src="https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=400" alt="Sofá moderno gris">
        <h3>Sofá Moderno Gris</h3>
        <p>Tela suave y estructura reforzada.</p>
        <div class="precio" aria-hidden="true">$450</div>
        <button class="btn-whatsapp" type="button">Pedir por WhatsApp</button>
    </div>

    <div class="producto" role="listitem" data-nombre="Lámpara de Pie Minimal" data-descripcion="Iluminación LED ajustable" data-precio="75">
        <img loading="lazy" src="https://images.unsplash.com/photo-1513507766391-aa3a70359f4a?w=400" alt="Lámpara minimal">
        <h3>Lámpara de Pie Minimal</h3>
        <p>Iluminación LED ajustable.</p>
        <div class="precio" aria-hidden="true">$75</div>
        <button class="btn-whatsapp" type="button">Pedir por WhatsApp</button>
    </div>

    <div class="producto" role="listitem" data-nombre="Silla Nórdica" data-descripcion="Madera de haya y diseño ergonómico" data-precio="120">
        <img loading="lazy" src="https://images.unsplash.com/photo-1592078615290-033ee584e267?w=400" alt="Silla nórdica">
        <h3>Silla Nórdica</h3>
        <p>Madera de haya y diseño ergonómico.</p>
        <div class="precio" aria-hidden="true">$120</div>
        <button class="btn-whatsapp" type="button">Pedir por WhatsApp</button>
    </div>
</section>

<div id="resultados-info" aria-live="polite" style="position:fixed;left:-9999px"></div>

<script>
  const buscador = document.getElementById('buscador');
  const productos = Array.from(document.getElementsByClassName('producto'));
  const info = document.getElementById('resultados-info');
  const telefono = '573001234567'; // Cambia esto si quieres otro número

  function filtrarProductos() {
    const filtro = buscador.value.trim().toLowerCase();
    let visibles = 0;
    productos.forEach(p => {
      const nombre = (p.dataset.nombre || '').toLowerCase();
      const descripcion = (p.dataset.descripcion || '').toLowerCase();
      const precio = (p.dataset.precio || '').toLowerCase();
      const hay = filtro === '' || nombre.includes(filtro) || descripcion.includes(filtro) || precio.includes(filtro);
      p.classList.toggle('oculto', !hay);
      if (hay) visibles++;
    });
    info.textContent = `${visibles} resultado(s)`;
    // aquí podrías mostrar un mensaje visible si visibles === 0
  }

  function debounce(fn, ms) {
    let t;
    return (...args) => {
      clearTimeout(t);
      t = setTimeout(() => fn(...args), ms);
    };
  }
  buscador.addEventListener('input', debounce(filtrarProductos, 200));

  document.getElementById('lista-productos').addEventListener('click', (e) => {
    const btn = e.target.closest('.btn-whatsapp');
    if (!btn) return;
    const producto = btn.closest('.producto');
    const nombre = producto.dataset.nombre;
    const precio = producto.dataset.precio;
    const mensaje = `Hola Hevemh Hogar, me interesa el producto: ${nombre} - Precio: $${precio}`;
    window.open(`https://wa.me/${telefono}?text=${encodeURIComponent(mensaje)}`, '_blank', 'noopener,noreferrer');
  });

  filtrarProductos();
</script>
</body>
</html>

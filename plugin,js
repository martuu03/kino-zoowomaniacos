// Plugin para Kino - zoowomaniacos.org

export async function home() {
  return [
    {
      title: "Últimos agregados",
      type: "row",
      items: await getCatalogItems("https://zoowomaniacos.org/")
    }
  ];
}

export async function search(query) {
  const url = `https://zoowomaniacos.org/?s=${encodeURIComponent(query)}`;
  return await getCatalogItems(url);
}

async function getCatalogItems(url) {
  try {
    const response = await fetch(url);
    const html = await response.text();
    
    const items = [];
    const regex = /<article[\s\S]*?<a href="([^"]+)"[\s\S]*?title="([^"]+)"[\s\S]*?(?:data-src|src)="([^"]+)"/g;
    let match;

    while ((match = regex.exec(html)) !== null) {
      items.push({
        id: match[1],
        title: match[2],
        poster: match[3],
        type: "movie"
      });
    }

    return items;
  } catch (error) {
    console.error("Error al obtener datos de zoowomaniacos:", error);
    return [];
  }
}

export async function resolve(id) {
  try {
    return {
      url: id,
      format: "mp4"
    };
  } catch (error) {
    throw new Error("No se pudo resolver el enlace");
  }
}

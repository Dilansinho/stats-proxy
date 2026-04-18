export default async function handler(req, res) {
  // CORS — permite llamadas desde cualquier origen (GitHub Pages, etc.)
  res.setHeader('Access-Control-Allow-Origin', '*');
  res.setHeader('Access-Control-Allow-Methods', 'GET, OPTIONS');
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type, x-apisports-key');

  if (req.method === 'OPTIONS') {
    return res.status(200).end();
  }

  // Parametros:
  //   path  = endpoint, ej: fixtures?league=140&season=2025&date=2026-04-18
  //   token = API key de api-football.com (apisports.io)
  const { path, token } = req.query;

  if (!path || !token) {
    return res.status(400).json({ error: 'Faltan parametros: path y token' });
  }

  try {
    const url = `https://v3.football.api-sports.io/${path}`;

    const response = await fetch(url, {
      method: 'GET',
      headers: {
        'x-apisports-key': token,
        'x-rapidapi-host': 'v3.football.api-sports.io',
      },
    });

    const data = await response.json();

    if (!response.ok) {
      return res.status(response.status).json(data);
    }

    return res.status(200).json(data);

  } catch (error) {
    return res.status(500).json({ error: 'Error del proxy: ' + error.message });
  }
}

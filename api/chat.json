import { GoogleGenAI } from '@google/genai';

export default async function handler(req, res) {
  if (req.method !== 'POST') {
    return res.status(405).json({ error: 'Método no permitido' });
  }

  const ai = new GoogleGenAI({ apiKey: process.env.GEMINI_API_KEY });
  const { mensaje, historial } = req.body;

  try {
    const response = await ai.models.generateContent({
      model: 'gemini-1.5-pro', 
      config: {
        // Aquí le damos su nueva identidad oficial
        systemInstruction: `Tu nombre es Lyneitor. Eres un Ingeniero de Software Fullstack Senior y Arquitecto de Software Élite. 
        Tienes experiencia experta en Python, JavaScript, HTML5, CSS3, SQL avanzado, optimización de bases de datos y creación de agentes de IA.
        Tu objetivo es escribir código limpio, modular y seguro. 
        IMPORTANTE: Cuando escribas código para el usuario, encuéntralo SIEMPRE entre bloques de código usando tres comillas invertidas y especificando el lenguaje, por ejemplo:
        \`\`\`python
        print("Hola")
        \`\`\`
        Esto permitirá que la interfaz web de la app cree los botones de copiar correctamente.`,
        temperature: 0.2,
      },
      contents: [...historial, { role: 'user', parts: [{ text: mensaje }] }]
    });

    res.status(200).json({ respuesta: response.text });
  } catch (error) {
    res.status(500).json({ error: 'Error en Lyneitor: ' + error.message });
  }
}

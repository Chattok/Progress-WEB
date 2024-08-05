const express = require('express');
const bodyParser = require('body-parser');
const axios = require('axios');

const app = express();
app.use(bodyParser.json());

app.post('/webhook', async (req, res) => {
    const message = req.body.Body; // Mensagem enviada pelo WhatsApp
    const from = req.body.From; // Número do remetente

    // Exemplo de chamada para uma API de geração de imagens
    const imageUrl = await generateImageFromPrompt(message);

    // Enviar a imagem de volta pelo WhatsApp
    await sendMessageWhatsApp(from, imageUrl);

    res.sendStatus(200);
});

async function generateImageFromPrompt(prompt) {
    const response = await axios.post('URL_DA_API_DE_GERACAO_DE_IMAGENS', {
        prompt: prompt
    });
    return response.data.imageUrl; // URL da imagem gerada
}

async function sendMessageWhatsApp(to, imageUrl) {
    await axios.post('URL_DA_API_DO_WHATSAPP', {
        to: to,
        type: 'image',
        image: {
            url: imageUrl
        }
    });
}

app.listen(3000, () => {
    console.log('Servidor rodando na porta 3000');
});

import discord
from discord import app_commands
import os
from dotenv import load_dotenv

load_dotenv()

DISCORD_TOKEN = os.getenv("DISCORD_TOKEN")

print(f"Token Discord: {DISCORD_TOKEN is not None}")

intents = discord.Intents.default()
intents.guilds = True
client = discord.Client(intents=intents)
tree = app_commands.CommandTree(client)

# 🔹 Comando /cambio_climatico
@tree.command(name="cambio_climatico", description="Información básica sobre el cambio climático")
async def cambio_climatico(interaction: discord.Interaction):
    parte1 = (
        "🌎 *¿Qué es el cambio climático?*\n\n"
        "El cambio climático se refiere a los cambios a largo plazo de las temperaturas y los patrones climáticos. "
        "Estos cambios pueden ser naturales, debido a variaciones en la actividad solar o erupciones volcánicas grandes. "
        "Pero desde el siglo XIX, las actividades humanas han sido el principal motor del cambio climático, debido principalmente a la quema de combustibles fósiles como el carbón, el petróleo y el gas.\n\n"
        "- La quema de combustibles fósiles genera emisiones de gases de efecto invernadero que actúan como una manta que envuelve a la Tierra.\n"
        "- Las emisiones principales son el dióxido de carbono y el metano, generadas por transporte, industria, agricultura y deforestación."
    )

    parte2 = (
        "⚠ *Causas principales:*\n"
        "- *Generación de energía:* Aún mucha electricidad proviene de carbón o gas, que emiten CO₂ y otros gases.\n"
        "- *Deforestación:* La tala de bosques libera el carbono almacenado. Se pierden ~12 millones de hectáreas al año.\n"
        "- *Uso de combustibles fósiles:* Camiones, barcos y aviones emiten grandes cantidades de gases contaminantes.\n\n"
        "❗ *Consecuencias:*\n"
        "- *Aumento del nivel del mar:* Por el calentamiento de los océanos.\n"
        "- *Olas de calor:* Las décadas recientes son las más cálidas registradas.\n"
        "- *Pérdida de biodiversidad:* Muchos ecosistemas no logran adaptarse a los cambios rápidos del clima."
    )

    parte3 = (
        "🌱 *Soluciones:*\n"
        "- *Energías renovables:* Sustituir carbón y gas por solar, eólica, etc.\n"
        "- *Reforestación:* Proteger y restaurar bosques.\n"
        "- *Cambios personales:* Usa transporte público, recicla, ahorra energía.\n\n"
        "📢 *Campañas globales:* Algunas organizaciones proponen proteger al menos el 30% del planeta para 2030.\n\n"
        "¡Protejamos nuestro planeta! 🌍"
    )

    await interaction.response.send_message(parte1)
    await interaction.followup.send(parte2)
    await interaction.followup.send(parte3)


# 🔹 Comando /reutilizar
@tree.command(name="reutilizar", description="Ideas para reutilizar un objeto o material en vez de tirarlo")
@app_commands.describe(objeto="Nombre del objeto (ej: caja, botella, lata, etc.)")
async def reutilizar(interaction: discord.Interaction, objeto: str):
    objeto = objeto.lower()

    ideas = {
        "caja": (
            "📦 *Reutilización de cajas:*\n"
            "- Cestas para ropa o libros.\n"
            "- Organizadores para zapatos.\n"
            "- Casitas para gatos o muñecos.\n"
            "- Laberintos para juegos educativos."
        ),
        "botella de plastico": (
            "🧴 *Botellas de plástico:*\n"
            "- Macetas colgantes o verticales.\n"
            "- Vasos o embudos caseros.\n"
            "- Riego por goteo para plantas.\n"
            "- Comederos para aves."
        ),
        "lata": (
            "🥫 *Latas de aluminio:*\n"
            "- Porta velas o faroles.\n"
            "- Organizador de escritorio.\n"
            "- Maceta pequeña decorativa.\n"
            "- Lámpara artesanal con luces LED."
        ),
        "papel": (
            "📄 *Papel reciclado:*\n"
            "- Notas reutilizables o bocetos.\n"
            "- Origami y manualidades.\n"
            "- Papel picado decorativo.\n"
            "- Envolver regalos."
        ),
        "carton": (
            "📦 *Cartón reutilizado:*\n"
            "- Maquetas escolares.\n"
            "- Estanterías pequeñas.\n"
            "- Disfraces caseros.\n"
            "- Juegos de mesa artesanales."
        ),
        "ropa": (
            "👕 *Ropa vieja:*\n"
            "- Cojines hechos con camisetas.\n"
            "- Bolsas de tela reutilizables.\n"
            "- Trapos para limpieza.\n"
            "- Fundas para celulares o lentes."
        ),
        "frascos": (
            "🍯 *Frascos de vidrio:*\n"
            "- Porta lápices o brochas.\n"
            "- Decoración con velas.\n"
            "- Almacenamiento de especias.\n"
            "- Mini invernaderos con tapa."
        ),
    }

    respuesta = ideas.get(objeto)
    if respuesta:
        await interaction.response.send_message(respuesta)
    else:
        await interaction.response.send_message(
            f"🤔 No tengo ideas para reutilizar *{objeto}* por ahora. ¡Pero usa tu imaginación y evita tirarlo!"
        )

# 🔹 Evento al iniciar
@client.event
async def on_ready():
    await tree.sync()
    print(f"✅ Bot conectado como {client.user}")

# 🔹 Ejecutar bot
client.run(token, jajaja no pondre mi token usen el suyo)

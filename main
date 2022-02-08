import discord
from discord import channel
from discord.embeds import Embed
from discord.ext import commands
import json
import asyncio
import mcstatus
import requests
import random
import youtube_dl

with open('setting.json', 'r', encoding='utf8') as jfile:
    data = json.load(jfile)

intents = discord.Intents.all()


bot = commands.Bot(command_prefix='!', intents=intents)


@bot.command()
async def ping(ctx):
    embed = discord.Embed(title=f'ping|延遲:{round(bot.latency * 150)}ms', colour=0x0000FF)
    await ctx.send(embed=embed)
    await ctx.message.delete()


@bot.event
async def on_ready():
    channel = bot.get_channel(869026698186850364)
    embed = discord.Embed(title=f">> Bot is ready <<", color=0x02d3f7)
    await channel.send(embed=embed)


@bot.event
async def on_member_join(Member):
    channel = bot.get_channel(876289890139127840)  # 1
    embed = discord.Embed(title=f"@{Member} (加入了)", colour=0x02d3f7)  # 1
    await channel.send(embed=embed)  # 1
    role = discord.utils.get(Member.guild.roles, name='players')  # 2
    await Member.add_roles(role)  # 2
    channele = bot.get_channel(897445041327456276)  # 3
    embed = discord.Embed(title=f"已為{Member}玩家增加players身份組", colour=0xff0000)
    await channele.send(embed=embed)
    embed = discord.Embed(title="歡迎加入NRTS伺服器", colour=0xff0000)
    await Member.send(embed=embed)


@bot.event
async def on_member_remove(member):
    channel = bot.get_channel(868378697533644810)
    embed = discord.Embed(title=f'@{member} (離開了)', colour=0x02d3f7)
    await channel.send(embed=embed)


@bot.command()
async def vote(ctx, *, message):
    embed = discord.Embed(title=f"{message}")
    msg = await ctx.channel.send(embed=embed)
    one = await msg.add_reaction('🇦')
    two = await msg.add_reaction('🇧')
    tree = await msg.add_reaction('🇨')
    WTF = await msg.add_reaction('🇩')
    await ctx.message.delete()
    try:
        secondint = 10
        seconds = 10
        if secondint > 1000:
            await ctx.send("jnra")
            raise BaseException
        if secondint <= 0:
            await ctx.send("grb")
            raise BaseException

        messsage = await ctx.send(f"投票餘下時間: {seconds}")

        while True:
            secondint -= 1
            if secondint == 0:
                await messsage.edit(content="投票結束!宣佈結果")
                await ctx.send(f"A={one}  B={two}  C={tree}  D={WTF}")
                break

            await messsage.edit(content=f"投票餘下時間: {secondint}")
            await asyncio.sleep(1)
    except ValueError:
        await ctx.send("hfagj")


@bot.command()
async def timee(ctx, seconds):
    try:
        await ctx.message.delete()
        secondint = int(seconds)
        if secondint > 10000000000:
            await ctx.send("時間不能超過1000秒也不能低於零秒")
            raise BaseException
        if secondint <= 0:
            await ctx.send("時間不能超過1000秒也不能低於零秒")
            raise BaseException

        yyds = await ctx.send(f"爆發倒數: {seconds}")

        while True:
            secondint -= 1
            if secondint == 0:
                await yyds.edit(content="時間結束!!!")
                break

            await yyds.edit(content=f"爆發倒數: {secondint}")
            await asyncio.sleep(1)
    except ValueError:
        await ctx.send("計時出現故障")


@bot.command()
async def time(ctx, seconds):
    try:
        await ctx.message.delete()
        secondint = int(seconds)
        if secondint > 1000000:
            await ctx.send("時間不能超過1000秒也不能低於零秒")
            raise BaseException
        if secondint <= 0:
            await ctx.send("時間不能超過1000秒也不能低於零秒")
            raise BaseException

        yyds = await ctx.send(f"剩餘時間: {seconds}")

        while True:
            secondint -= 1
            if secondint == 0:
                await yyds.edit(content="時間結束!!!")
                break

            await yyds.edit(content=f"剩餘時間: {secondint}")
            await asyncio.sleep(1)
    except ValueError:
        await ctx.send("計時出現故障")


@bot.command()
async def online(ctx, message):
    try:
        server = MinecraftServer.lookup(f"{message}")
        status = server.status()
        qqww = status.Version
        OKL = status.players.online
        hyut = status.latency
        embed = discord.Embed(title=f"伺服器|server:{message} \n 伺服器當前玩家在線人數|players online:{OKL} \n 伺服器延遲|server ping:{hyut} \n 版本|Version:{qqww}")
        await ctx.send(embed=embed)
        await ctx.message.delete()
    except ValueError:
        await ctx.send(f"沒有這個伺服器{message}")
        await ctx.message.delete()


@bot.command()
async def helpp(ctx):
    embed = discord.Embed(title="----------機械人功能介紹----------", description="1.機械人擁有玩家加入或退出訊息 \n 2.機械人擁有舉辦投票功能(!vote {"
                                                                           "message}) \n 3.機械人擁有計時功能(!time {"
                                                                           "seconds})) \n "
                                                                           "4.機械人可以查詢1.7版本以上的任何一個minecraft伺服器的線上人數("
                                                                           "!online {server ip}) \n "
                                                                           "5.機械人可以使用minecraft id查詢UUID(!players {"
                                                                           "minecraftID}) \n "
                                                                           "6. 機械人可以使用隨機數(1-100)(!lucky) \n "
                                                                           "----------機械人其他功能還在開發中----------")
    await ctx.send(embed=embed)
    await ctx.message.delete()


@bot.command()
async def players(ctx, message1):
    try:
        url = requests.get(f"https://api.mojang.com/users/profiles/minecraft/{message1}?").json()
        id = url['id']
        embed = discord.Embed(title=f"Name:{message1} \n ID:{id}")
        await ctx.send(embed=embed)
        await ctx.message.delete()
    except ValueError:
        embed = discord.Embed(title=f"沒有這位玩家{message1}")
        await ctx.send(embed=embed)
        await ctx.message.delete()


@bot.command()
async def lucky(ctx):
  ii = "%"
  fuck = random.randint(0,100)
  try:
    embed = discord.Embed(title=f"{fuck}{ii}")
    await ctx.send(embed=embed)
  except ValueError:
    embed = discord.Embed(title="error")
    await ctx.send(embed=embed)

bot.run(data['TOKEN'])


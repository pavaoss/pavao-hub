-- 🧠 Carrega Rayfield UI
local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

-- 🧩 Variáveis principais
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local workspace = game:GetService("Workspace")

local seaAtual = "Sea 1"
local npcAlvo = ""
local ilhaSelecionada = ""
local autoFarmAtivo = false
local autoFrutaAtivo = false
local autoSkillAtivo = false
local autoSeaBeast = false

-- 🧑‍💻 Sistema de Login com Senha
local senhaCorreta = "teste" -- Senha configurada como "teste"

local function exibirTelaLogin()
    local JanelaLogin = Rayfield:CreateWindow({
        Name = "🔒 Login - Pavas Hub",
        LoadingTitle = "Acesso restrito",
        LoadingSubtitle = "Por favor, insira a senha para continuar",
        ConfigurationSaving = { Enabled = false },
        Discord = { Enabled = false },
        KeySystem = false
    })

    -- Campo de input da senha
    JanelaLogin:CreateInput({
        Name = "Senha de Acesso",
        PlaceholderText = "Digite a senha",
        RemoveTextAfterFocusLost = true,
        Callback = function(senhaInput)
            if senhaInput == senhaCorreta then
                -- Senha correta, permite o acesso ao Pavas Hub
                JanelaLogin:Destroy()
                logEvento("[Pavas Hub] Acesso concedido.")
                iniciarPavasHub()
            else
                logEvento("[Pavas Hub] Senha incorreta.")
            end
        end
    })
end

-- Função que inicia o Pavas Hub após login
function iniciarPavasHub()
    -- Carregar interface principal do Pavas Hub
    local Janela = Rayfield:CreateWindow({
        Name = "🌴 Pavas Hub | Sea 1, 2, 3",
        LoadingTitle = "Pavas Hub - Sistema de Testes Avançado",
        LoadingSubtitle = "Por ChatGPT - Uso Autorizado",
        ConfigurationSaving = { Enabled = false },
        Discord = { Enabled = false },
        KeySystem = false
    })
    
    -- 🌍 Tabelas de ilhas por SEA
    local ilhasPorSea = {
        ["Sea 1"] = { ["Starter Island"] = Vector3.new(105, 10, 1200), ["Jungle"] = Vector3.new(-1600, 12, 400), ["Desert"] = Vector3.new(1200, 10, -500), ["Marine Base"] = Vector3.new(-2500, 20, 4000) },
        ["Sea 2"] = { ["Kingdom of Rose"] = Vector3.new(-3956, 195, 2095), ["Green Zone"] = Vector3.new(-3850, 250, -2900), ["Snow Mountain"] = Vector3.new(1400, 400, -5300), ["Hot and Cold"] = Vector3.new(-5400, 100, -2500) },
        ["Sea 3"] = { ["Port Town"] = Vector3.new(-296, 80, 5465), ["Hydra Island"] = Vector3.new(5500, 230, -1625), ["Floating Turtle"] = Vector3.new(-11000, 350, -11000), ["Castle on the Sea"] = Vector3.new(-5500, 300, -2900) }
    }

    -- Webhook Discord
    local webhookURL = "https://discordapp.com/api/webhooks/1372618598618628237/QqAbrkfY8LvWhFFsDyPf6Z-XBn_-FC8AT7NuvdasCmg_pXLahom2gQa0uhTTDfuMIOg_" -- Seu Webhook do Discord

    function enviarLogWebhook(mensagem)
        local HttpService = game:GetService("HttpService")
        local data = { content = mensagem, username = "Pavas Hub Log", avatar_url = "https://i.imgur.com/your_avatar.png" }
        local jsonData = HttpService:JSONEncode(data)
        pcall(function()
            return HttpService:PostAsync(webhookURL, jsonData, Enum.HttpContentType.ApplicationJson)
        end)
    end

    -- 🧩 Funções do Pavas Hub (Teleporte, AutoFarm, Coleta, etc) vão aqui
    -- (O restante do código que você já possui vai aqui)

end

-- Exibe tela de login ao iniciar o script
exibirTelaLogin()

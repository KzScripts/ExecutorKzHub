local TweenService = game:GetService("TweenService")
local player = game:GetService("Players").LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local UserInputService = game:GetService("UserInputService")

-- Cores modernas
local cores = {
    fundo = Color3.fromRGB(20, 20, 25),
    titulo = Color3.fromRGB(25, 25, 35),
    botao = Color3.fromRGB(45, 45, 60),
    botaoHover = Color3.fromRGB(55, 55, 75),
    editor = Color3.fromRGB(18, 18, 22),
    texto = Color3.fromRGB(220, 220, 220),
    textoSecundario = Color3.fromRGB(160, 160, 160),
    verde = Color3.fromRGB(40, 200, 80),
    vermelho = Color3.fromRGB(200, 50, 50),
    azul = Color3.fromRGB(60, 120, 200)
}

-- GUI Principal
local gui = Instance.new("ScreenGui")
gui.Name = "KzHubVortex"
gui.ResetOnSpawn = false
gui.Parent = playerGui

-- Frame Principal
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 650, 0, 380)
mainFrame.Position = UDim2.new(0.5, -325, 0.5, -190)
mainFrame.BackgroundColor3 = cores.fundo
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = gui

-- Sombra
local shadow = Instance.new("Frame")
shadow.Size = UDim2.new(1, 6, 1, 6)
shadow.Position = UDim2.new(0, -3, 0, -3)
shadow.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
shadow.BackgroundTransparency = 0.8
shadow.BorderSizePixel = 0
shadow.ZIndex = -1
shadow.Parent = mainFrame
Instance.new("UICorner", shadow).CornerRadius = UDim.new(0, 12)

Instance.new("UICorner", mainFrame).CornerRadius = UDim.new(0, 10)

-- Barra de Título
local titleBar = Instance.new("Frame")
titleBar.Size = UDim2.new(1, 0, 0, 35)
titleBar.BackgroundColor3 = cores.titulo
titleBar.BorderSizePixel = 0
titleBar.Parent = mainFrame
Instance.new("UICorner", titleBar).CornerRadius = UDim.new(0, 10)

-- Logo e Título
local logo = Instance.new("ImageLabel")
logo.Size = UDim2.new(0, 20, 0, 20)
logo.Position = UDim2.new(0, 10, 0.5, -10)
logo.Image = "rbxassetid://71567579053009"
logo.BackgroundTransparency = 1
logo.Parent = titleBar

local titulo = Instance.new("TextLabel")
titulo.Size = UDim2.new(1, -150, 1, 0)
titulo.Position = UDim2.new(0, 35, 0, 0)
titulo.BackgroundTransparency = 1
titulo.Text = "Kz Hub Vortex - Script Executor"
titulo.TextColor3 = cores.texto
titulo.Font = Enum.Font.GothamBold
titulo.TextSize = 14
titulo.TextXAlignment = Enum.TextXAlignment.Left
titulo.Parent = titleBar

-- Botões da Barra de Título
local function criarBotaoTitulo(pos, cor, texto)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 25, 0, 25)
    btn.Position = pos
    btn.BackgroundColor3 = cor
    btn.Text = texto
    btn.TextColor3 = cores.texto
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 12
    btn.BorderSizePixel = 0
    btn.Parent = titleBar
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 4)
    return btn
end

local minimizeBtn = criarBotaoTitulo(UDim2.new(1, -80, 0.5, -12.5), cores.azul, "_")
local closeBtn = criarBotaoTitulo(UDim2.new(1, -50, 0.5, -12.5), cores.vermelho, "X")

-- Container Principal
local container = Instance.new("Frame")
container.Size = UDim2.new(1, -20, 1, -45)
container.Position = UDim2.new(0, 10, 0, 40)
container.BackgroundTransparency = 1
container.Parent = mainFrame

-- Abas
local tabContainer = Instance.new("Frame")
tabContainer.Size = UDim2.new(1, 0, 0, 30)
tabContainer.BackgroundTransparency = 1
tabContainer.Parent = container

local function criarAba(pos, texto, ativo)
    local aba = Instance.new("TextButton")
    aba.Size = UDim2.new(0, 70, 1, 0)
    aba.Position = pos
    aba.BackgroundColor3 = ativo and cores.botao or cores.titulo
    aba.Text = texto
    aba.TextColor3 = cores.texto
    aba.Font = Enum.Font.Gotham
    aba.TextSize = 10
    aba.BorderSizePixel = 0
    aba.Parent = tabContainer
    Instance.new("UICorner", aba).CornerRadius = UDim.new(0, 6)
    return aba
end

local abaEditor = criarAba(UDim2.new(0, 0, 0, 0), "Editor", true)
local abaScripts = criarAba(UDim2.new(0, 75, 0, 0), "Scripts", false)

-- Editor de Código
local editorFrame = Instance.new("Frame")
editorFrame.Size = UDim2.new(1, 0, 1, -70)
editorFrame.Position = UDim2.new(0, 0, 0, 35)
editorFrame.BackgroundColor3 = cores.editor
editorFrame.BorderSizePixel = 0
editorFrame.Parent = container
Instance.new("UICorner", editorFrame).CornerRadius = UDim.new(0, 8)

-- Números de Linha
local lineNumbers = Instance.new("TextLabel")
lineNumbers.Size = UDim2.new(0, 30, 1, -10)
lineNumbers.Position = UDim2.new(0, 5, 0, 5)
lineNumbers.BackgroundTransparency = 1
lineNumbers.Text = "1\n2\n3\n4\n5\n6\n7\n8\n9\n10"
lineNumbers.TextColor3 = cores.textoSecundario
lineNumbers.Font = Enum.Font.RobotoMono
lineNumbers.TextSize = 10
lineNumbers.TextYAlignment = Enum.TextYAlignment.Top
lineNumbers.Parent = editorFrame

-- Separador
local separator = Instance.new("Frame")
separator.Size = UDim2.new(0, 1, 1, -10)
separator.Position = UDim2.new(0, 35, 0, 5)
separator.BackgroundColor3 = cores.textoSecundario
separator.BorderSizePixel = 0
separator.Parent = editorFrame

-- Caixa de Código
local codeBox = Instance.new("TextBox")
codeBox.Size = UDim2.new(1, -45, 1, -10)
codeBox.Position = UDim2.new(0, 40, 0, 5)
codeBox.BackgroundTransparency = 1
codeBox.TextColor3 = cores.texto
codeBox.ClearTextOnFocus = false
codeBox.MultiLine = true
codeBox.TextWrapped = true
codeBox.Text = "-- Bem-vindo ao Kz Hub Vortex!\n-- Cole seu script aqui e clique em Executar\n\nprint('Hello World!')"
codeBox.TextXAlignment = Enum.TextXAlignment.Left
codeBox.TextYAlignment = Enum.TextYAlignment.Top
codeBox.Font = Enum.Font.RobotoMono
codeBox.TextSize = 10
codeBox.Parent = editorFrame

-- Barra de Status
local statusBar = Instance.new("Frame")
statusBar.Size = UDim2.new(1, 0, 0, 20)
statusBar.Position = UDim2.new(0, 0, 1, -20)
statusBar.BackgroundColor3 = cores.titulo
statusBar.BorderSizePixel = 0
statusBar.Parent = editorFrame

local statusText = Instance.new("TextLabel")
statusText.Size = UDim2.new(1, -10, 1, 0)
statusText.Position = UDim2.new(0, 5, 0, 0)
statusText.BackgroundTransparency = 1
statusText.Text = "Pronto"
statusText.TextColor3 = cores.textoSecundario
statusText.Font = Enum.Font.Gotham
statusText.TextSize = 10
statusText.TextXAlignment = Enum.TextXAlignment.Left
statusText.Parent = statusBar

Instance.new("UICorner", statusBar).CornerRadius = UDim.new(0, 6)

-- Botões de Ação
local buttonFrame = Instance.new("Frame")
buttonFrame.Size = UDim2.new(1, 0, 0, 30)
buttonFrame.Position = UDim2.new(0, 0, 1, -30)
buttonFrame.BackgroundTransparency = 1
buttonFrame.Parent = container

local function criarBotaoAcao(pos, size, texto, cor)
    local btn = Instance.new("TextButton")
    btn.Size = size
    btn.Position = pos
    btn.BackgroundColor3 = cor
    btn.Text = texto
    btn.TextColor3 = cores.texto
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 10
    btn.BorderSizePixel = 0
    btn.Parent = buttonFrame
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)
    
    -- Efeito hover
    btn.MouseEnter:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = cores.botaoHover}):Play()
    end)
    btn.MouseLeave:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = cor}):Play()
    end)
    
    return btn
end

local executeBtn = criarBotaoAcao(UDim2.new(0, 0, 0, 0), UDim2.new(0.23, 0, 1, 0), "Executar", cores.verde)
local clearBtn = criarBotaoAcao(UDim2.new(0.26, 0, 0, 0), UDim2.new(0.22, 0, 1, 0), "Limpar", cores.vermelho)
local saveBtn = criarBotaoAcao(UDim2.new(0.51, 0, 0, 0), UDim2.new(0.22, 0, 1, 0), "Salvar", cores.azul)
local loadBtn = criarBotaoAcao(UDim2.new(0.76, 0, 0, 0), UDim2.new(0.24, 0, 1, 0), "Carregar", cores.botao)

-- Notificação
local notificationFrame = Instance.new("Frame")
notificationFrame.Size = UDim2.new(0, 300, 0, 60)
notificationFrame.Position = UDim2.new(1, -320, 0, 20)
notificationFrame.BackgroundColor3 = cores.fundo
notificationFrame.BorderSizePixel = 0
notificationFrame.Visible = false
notificationFrame.Parent = gui
Instance.new("UICorner", notificationFrame).CornerRadius = UDim.new(0, 8)

local notificationText = Instance.new("TextLabel")
notificationText.Size = UDim2.new(1, -20, 1, 0)
notificationText.Position = UDim2.new(0, 10, 0, 0)
notificationText.BackgroundTransparency = 1
notificationText.Text = ""
notificationText.TextColor3 = cores.texto
notificationText.Font = Enum.Font.Gotham
notificationText.TextSize = 12
notificationText.TextWrapped = true
notificationText.Parent = notificationFrame

-- Logo Minimizado
local logoMinimizado = Instance.new("ImageButton")
logoMinimizado.Size = UDim2.new(0, 50, 0, 50)
logoMinimizado.Position = UDim2.new(0, 20, 0, 20)
logoMinimizado.Image = "rbxassetid://71567579053009"
logoMinimizado.BackgroundColor3 = cores.fundo
logoMinimizado.BorderSizePixel = 0
logoMinimizado.Visible = false
logoMinimizado.Active = true
logoMinimizado.Draggable = true
logoMinimizado.Parent = gui
Instance.new("UICorner", logoMinimizado).CornerRadius = UDim.new(1, 0)

-- Variáveis de controle
local scriptsSalvos = {}
local scriptAtual = ""

-- Funções
local function mostrarNotificacao(texto, cor)
    notificationFrame.BackgroundColor3 = cor or cores.fundo
    notificationText.Text = texto
    notificationFrame.Visible = true
    
    TweenService:Create(notificationFrame, TweenInfo.new(0.3), {Position = UDim2.new(1, -320, 0, 20)}):Play()
    
    wait(2)
    
    TweenService:Create(notificationFrame, TweenInfo.new(0.3), {Position = UDim2.new(1, 0, 0, 20)}):Play()
    wait(0.3)
    notificationFrame.Visible = false
end

local function atualizarLinhas()
    local linhas = codeBox.Text:split("\n")
    local numeroLinhas = ""
    for i = 1, #linhas do
        numeroLinhas = numeroLinhas .. tostring(i) .. "\n"
    end
    lineNumbers.Text = numeroLinhas
end

local function atualizarStatus(texto)
    statusText.Text = texto
end

-- Eventos dos Botões
executeBtn.MouseButton1Click:Connect(function()
    local code = codeBox.Text
    if code == "" then
        mostrarNotificacao(" Nenhum código para executar!", cores.vermelho)
        return
    end
    
    atualizarStatus("Executando...")
    mostrarNotificacao(" Executando script...", cores.azul)
    
    local success, err = pcall(function()
        loadstring(code)()
    end)
    
    if success then
        atualizarStatus("Executado com sucesso")
        mostrarNotificacao(" Script executado com sucesso!", cores.verde)
    else
        atualizarStatus("Erro na execução")
        mostrarNotificacao(" Erro: " .. tostring(err), cores.vermelho)
        warn("Executor Error:", err)
    end
end)

clearBtn.MouseButton1Click:Connect(function()
    codeBox.Text = ""
    atualizarLinhas()
    atualizarStatus("Editor limpo")
    mostrarNotificacao(" Editor limpo!", cores.azul)
end)

saveBtn.MouseButton1Click:Connect(function()
    if codeBox.Text ~= "" then
        scriptAtual = codeBox.Text
        table.insert(scriptsSalvos, scriptAtual)
        atualizarStatus("Script salvo")
        mostrarNotificacao(" Script salvo!", cores.verde)
    else
        mostrarNotificacao(" Nada para salvar!", cores.vermelho)
    end
end)

loadBtn.MouseButton1Click:Connect(function()
    if #scriptsSalvos > 0 then
        codeBox.Text = scriptsSalvos[#scriptsSalvos]
        atualizarLinhas()
        atualizarStatus("Script carregado")
        mostrarNotificacao(" Script carregado!", cores.verde)
    else
        mostrarNotificacao("Nenhum script salvo!", cores.vermelho)
    end
end)

minimizeBtn.MouseButton1Click:Connect(function()
    local tween = TweenService:Create(mainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
        Size = UDim2.new(0, 0, 0, 0),
        Position = UDim2.new(0.5, 0, 0.5, 0)
    })
    tween:Play()
    tween.Completed:Connect(function()
        mainFrame.Visible = false
        logoMinimizado.Visible = true
    end)
end)

closeBtn.MouseButton1Click:Connect(function()
    gui:Destroy()
end)

logoMinimizado.MouseButton1Click:Connect(function()
    mainFrame.Visible = true
    mainFrame.Size = UDim2.new(0, 0, 0, 0)
    mainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
    
    local tween = TweenService:Create(mainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
        Size = UDim2.new(0, 650, 0, 380),
        Position = UDim2.new(0.5, -325, 0.5, -190)
    })
    tween:Play()
    logoMinimizado.Visible = false
end)

-- Atualizar linhas quando o texto mudar
codeBox:GetPropertyChangedSignal("Text"):Connect(atualizarLinhas)

-- Atalhos de teclado
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    
    if input.KeyCode == Enum.KeyCode.F9 then
        executeBtn.MouseButton1Click()
    elseif input.KeyCode == Enum.KeyCode.F5 then
        clearBtn.MouseButton1Click()
    end
end)

-- Inicialização
atualizarLinhas()
atualizarStatus("Kz Hub Vortex carregado - Pressione F9 para executar")
mostrarNotificacao(" Kz Hub Vortex carregado!", cores.verde)

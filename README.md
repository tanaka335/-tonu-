local P=game.Players;local RS=game:GetService"RunService";local U=game:GetService"UserInputService"
local p=P.LocalPlayer;c=workspace.CurrentCamera;e=true;a=.28;s=.23;m=300;f=85;l=20
local g=Instance.new"ScreenGui";g.Name="WeakAimAssist";g.ResetOnSpawn=false;g.Parent=p:WaitForChild"PlayerGui"
local t=Instance.new"TextLabel";t.Size=UDim2.new(0,360,0,60);t.Position=UDim2.new(0,20,0,20)
t.BackgroundColor3=Color3.fromRGB(20,20,20);t.BackgroundTransparency=.3;t.TextColor3=Color3.fromRGB(0,255,100)
t.TextScaled=true;t.Font=Enum.Font.GothamBold;t.Parent=g
local d=Instance.new"TextLabel";d.Size=UDim2.new(0,360,0,50);d.Position=UDim2.new(0,20,0,90)
d.BackgroundColor3=Color3.fromRGB(30,30,30);d.BackgroundTransparency=.4;d.TextColor3=Color3.fromRGB(255,255,100)
d.TextScaled=true;d.Font=Enum.Font.Gotham;d.Parent=g
local x=Instance.new"Frame";x.Size=UDim2.new(0,36,0,36);x.Position=UDim2.new(.5,0,.5,0)
x.AnchorPoint=Vector2.new(.5,.5);x.BackgroundTransparency=1;x.Parent=g
local h=Instance.new"Frame";h.Size=UDim2.new(1,0,0,3);h.BackgroundColor3=Color3.fromRGB(255,60,60)
h.Position=UDim2.new(0,0,.5,-1.5);h.Parent=x
local v=Instance.new"Frame";v.Size=UDim2.new(0,3,1,0);v.BackgroundColor3=Color3.fromRGB(255,60,60)
v.Position=UDim2.new(.5,-1.5,0,0);v.Parent=x
local b=Instance.new"TextButton";b.Size=UDim2.new(0,180,0,80);b.Position=UDim2.new(1,-200,0,30)
b.BackgroundColor3=Color3.fromRGB(0,170,0);b.TextColor3=Color3.new(1,1,1);b.TextScaled=true
b.Font=Enum.Font.GothamBold;b.Text="Aim Assist: ON";b.Parent=g;Instance.new("UICorner",b).CornerRadius=UDim.new(0,16)
local q=Instance.new"Frame";q.Size=UDim2.new(0,420,0,70);q.Position=UDim2.new(.5,-210,1,-90)
q.BackgroundColor3=Color3.fromRGB(25,25,25);q.Parent=g
local sl=Instance.new"TextLabel";sl.Size=UDim2.new(1,0,0,25);sl.BackgroundTransparency=1
sl.Text="視野角 (FOV Angle): "..f;sl.TextColor3=Color3.new(1,1,1);sl.TextScaled=true;sl.Font=Enum.Font.GothamBold;sl.Parent=q
local r=Instance.new"Frame";r.Size=UDim2.new(1,-40,0,12);r.Position=UDim2.new(0,20,.5,-6)
r.BackgroundColor3=Color3.fromRGB(60,60,60);r.Parent=q
local i=Instance.new"Frame";i.Size=UDim2.new(.5,0,1,0);i.BackgroundColor3=Color3.fromRGB(0,170,255);i.Parent=r
local k=Instance.new"Frame";k.Size=UDim2.new(0,24,1,0);k.Position=UDim2.new(.5,-12,0,0)
k.BackgroundColor3=Color3.fromRGB(255,255,255);k.Parent=r;Instance.new("UICorner",k).CornerRadius=UDim.new(1,0)
local function us()local z=(f-30)/90;i.Size=UDim2.new(z,0,1,0);k.Position=UDim2.new(z,-12,0,0)
sl.Text="視野角 (FOV Angle): "..math.floor(f)end
local y=false;k.InputBegan:Connect(function(n)if n.UserInputType==Enum.UserInputType.MouseButton1 or n.UserInputType==Enum.UserInputType.Touch then y=true end end)
U.InputChanged:Connect(function(n)if not y then return end
if n.UserInputType==Enum.UserInputType.MouseMovement or n.UserInputType==Enum.UserInputType.Touch then
local mx=n.Position.X;local bx=r.AbsolutePosition.X;local bs=r.AbsoluteSize.X
local z=math.clamp((mx-bx)/bs,0,1);f=30+z*90;us()end end)
U.InputEnded:Connect(function(n)if n.UserInputType==Enum.UserInputType.MouseButton1 or n.UserInputType==Enum.UserInputType.Touch then y=false end end)
local function gt()local bt,bd,ba=nil,math.huge,f;for _,o in P:GetPlayers()do
if o~=p and o.Character and o.Character:FindFirstChild"HumanoidRootPart"then local rt=o.Character.HumanoidRootPart
local dd=(rt.Position-c.CFrame.Position).Magnitude;if dd<=m then local di=(rt.Position-c.CFrame.Position).Unit
local aa=math.deg(math.acos(c.CFrame.LookVector:Dot(di)))if aa<ba and dd<bd then ba=aa;bd=dd;bt=rt end end end end
return bt,bd end
local function uu()b.BackgroundColor3=e and Color3.fromRGB(0,170,0)or Color3.fromRGB(170,0,0)
b.Text=e and"Aim Assist: ON"or"Aim Assist: OFF"end
RS.RenderStepped:Connect(function()
local tt,nd=gt()if tt and e then local dt=(tt.Position-c.CFrame.Position).Unit;_G.W=c.CFrame.LookVector:Lerp(dt,a)
if nd<=l then local tp=tt.Position+Vector3.new(0,2,0)local dc=CFrame.lookAt(c.CFrame.Position,tp)
c.CFrame=c.CFrame:Lerp(dc,s)h.BackgroundColor3=Color3.fromRGB(80,255,80)v.BackgroundColor3=Color3.fromRGB(80,255,80)
t.Text="✅ 10studs以内！視点追従中"else h.BackgroundColor3=Color3.fromRGB(255,200,60)v.BackgroundColor3=Color3.fromRGB(255,200,60)
t.Text="Aim Assist: ON (近くで視点追従)"end
d.Text="🎯 Target: "..tt.Parent.Name.." | 距離: "..string.format("%.1f",nd).." studs | FOV: "..f else
_G.W=c.CFrame.LookVector;h.BackgroundColor3=Color3.fromRGB(255,60,60)v.BackgroundColor3=Color3.fromRGB(255,60,60)
t.Text="Aim Assist: "..(e and"ON"or"OFF")d.Text="Debug: 他のP "..(#P:GetPlayers()-1).."人 | 最寄り "..(nd or 999).." studs | FOV: "..f end
x.Visible=e end)
b.Activated:Connect(function()e=not e;uu()end)
U.InputBegan:Connect(function(i,g)if g or i.KeyCode~=Enum.KeyCode.F then return end;e=not e;uu()end)
uu();us();print"ロード完了"

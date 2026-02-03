-- Character Creation
local player = {
    name = "Player",
    level = 1,
    experience = 0,
    maxHealth = 100,
    currentHealth = 100,
    maxStamina = 100,
    currentStamina = 100,
    maxMoney = 0,
    currentMoney = 0,
    inventory = {}
}

-- Function to create a new character
function createCharacter(name)
    player.name = name
    print("Character created successfully!")
end

-- Function to check character level
function checkLevel()
    if player.experience >= 100 then
        player.level = player.level + 1
        player.experience = player.experience - 100
        print("You leveled up!")
    end
end

-- Function to check character health
function checkHealth()
    if player.currentHealth <= 0 then
        print("You died!")
    elseif player.currentHealth < player.maxHealth then
        print("You are wounded!")
    else
        print("You are healthy!")
    end
end

-- Function to check character stamina
function checkStamina()
    if player.currentStamina <= 0 then
        print("You are exhausted!")
    elseif player.currentStamina < player.maxStamina then
        print("You are tired!")
    else
        print("You are energized!")
    end
end

-- Function to check character money
function checkMoney()
    if player.currentMoney <= 0 then
        print("You have no money!")
    else
        print("You have money!")
    end
end

-- Function to add money to character
function addMoney(amount)
    player.currentMoney = player.currentMoney + amount
    print("You added money to your inventory!")
end

-- Function to remove money from character
function removeMoney(amount)
    if player.currentMoney >= amount then
        player.currentMoney = player.currentMoney - amount
        print("You removed money from your inventory!")
    else
        print("You don't have enough money!")
    end
end

-- Function to add item to character inventory
function addItem(name, quantity)
    table.insert(player.inventory, {name = name, quantity = quantity})
    print("You added " .. name .. " to your inventory!")
end

-- Function to remove item from character inventory
function removeItem(name)
    for i, v in pairs(player.inventory) do
        if v.name == name then
            table.remove(player.inventory, i)
            print("You removed " .. name .. " from your inventory!")
            return
        end
    end
    print("You don't have " .. name .. " in your inventory!")
end

-- Function to check character inventory
function checkInventory()
    for i, v in pairs(player.inventory) do
        print(v.name .. " x" .. v.quantity)
    end
end

-- Function to exit the game
function exitGame()
    print("You left the game!")
    os.exit()
end

-- Main game function
function main()
    print("Welcome to Blox Fruit!")
    createCharacter("Player")
    while true do
        print("\n1 - Check level")
        print("2 - Check health")
        print("3 - Check stamina")
        print("4 - Check money")
        print("5 - Add money")
        print("6 - Remove money")
        print("7 - Add item")
        print("8 - Remove item")
        print("9 - Check inventory")
        print("10 - Exit game")
        
        local choice = io.read()
        
        if choice == "1" then
            checkLevel()
        elseif choice == "2" then
            checkHealth()
        elseif choice == "3" then
            checkStamina()
        elseif choice == "4" then
            checkMoney()
        elseif choice == "5" then
            addMoney(100)
        elseif choice == "6" then
            removeMoney(100)
        elseif choice == "7" then
            addItem("Item", 10)
        elseif choice == "8" then
            removeItem("Item")
        elseif choice == "9" then
            checkInventory()
        elseif choice == "10" then
            exitGame()
        else
            print("Invalid option!")
        end
    end
end

main()

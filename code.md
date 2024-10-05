# 假设使用Python编写后端逻辑
import random

def generate_game_name(length=5, include_numbers=False, include_special_chars=False):
    words = ["Warrior", "Mage", "Rogue", "Dragon", "Phoenix", "Shadow", "Light"]
    numbers = "0123456789"
    special_chars = "!@#$%^&*()_+"
    
    name = ""
    for _ in range(length):
        if random.choice([True, False]):
            name += random.choice(words)
        else:
            if include_numbers:
                name += random.choice(numbers)
            elif include_special_chars:
                name += random.choice(special_chars)
            else:
                name += random.choice("ABCDEFGHIJKLMNOPQRSTUVWXYZ")
    
    return name

# 用户请求生成游戏名
user_request = {
    "length": 6,
    "include_numbers": True,
    "include_special_chars": True
}

game_name = generate_game_name(**user_request)
print(game_name)
# 生成游戏名的函数

def generate_game_name_v2(length=5, include_numbers=False, include_special_chars=False, num_words=1, num_numbers=0, num_special_chars=0):
    """
    生成游戏名的函数。
    :param length: 名字的总长度。
    :param include_numbers: 是否包含数字。
    :param include_special_chars: 是否包含特殊字符。
    :param num_words: 单词的数量。
    :param num_numbers: 数字的个数。
    :param num_special_chars: 特殊字符的个数。
    :return: 生成的游戏名。
    """
    words = ["Warrior", "Mage", "Rogue", "Dragon", "Phoenix", "Shadow", "Light"]
    numbers = "0123456789"
    special_chars = "!@#$%^&*()_+"

    # 确保单词、数字和特殊字符的总数不超过名字的长度
    if num_words + num_numbers + num_special_chars > length:
        raise ValueError("总数不能超过名字的长度")

    name_parts = []

    # 添加单词
    for _ in range(num_words):
        name_parts.append(random.choice(words))

    # 添加数字
    for _ in range(num_numbers):
        name_parts.append(random.choice(numbers))

    # 添加特殊字符
    for _ in range(num_special_chars):
        name_parts.append(random.choice(special_chars))

    # 如果还有空位，随机添加单词或字母
    for _ in range(length - len(name_parts)):
        if random.choice([True, False]):
            name_parts.append(random.choice(words))
        else:
            name_parts.append(random.choice("ABCDEFGHIJKLMNOPQRSTUVWXYZ"))

    # 打乱顺序并组合成名字
    random.shuffle(name_parts)
    game_name = "".join(name_parts)

    # 如果最终长度超过预期，截断
    if len(game_name) > length:
        game_name = game_name[:length]

    return game_name

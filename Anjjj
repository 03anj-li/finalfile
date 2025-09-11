from PIL import Image, ImageDraw, ImageFont

def generate_policy_arrow(policy_term=20, premium_years=10,
                          arrow_path="arrow.png", coin_path="coin.png",
                          output_path="output.png"):
    # Load arrow and coin images
    arrow = Image.open(arrow_path).convert("RGBA")
    coin = Image.open(coin_path).convert("RGBA")

    # Resize arrow proportionally to policy term
    base_width = policy_term * 40   # scale factor: 40px per year
    arrow = arrow.resize((base_width, 60))  # height fixed

    # Create blank canvas
    canvas_height = 200
    canvas = Image.new("RGBA", (base_width + 100, canvas_height), (255, 255, 255, 0))

    # Paste arrow onto canvas (centered vertically)
    canvas.paste(arrow, (50, 80), arrow)

    # Draw numbers on arrow
    draw = ImageDraw.Draw(canvas)
    try:
        font = ImageFont.truetype("arial.ttf", 18)
    except:
        font = ImageFont.load_default()

    step = base_width // policy_term
    for i in range(policy_term):
        x = 50 + (i * step) + step // 2
        draw.text((x, 150), str(i+1), fill="black", font=font, anchor="mm")

    # Place coins for premium years
    coin = coin.resize((30, 30))
    for i in range(premium_years):
        x = 50 + (i * step) + step // 2 - 15
        y = 40
        canvas.paste(coin, (x, y), coin)

    # Save result
    canvas.save(output_path)
    print(f"Saved timeline to {output_path}")


# Example usage:
generate_policy_arrow(policy_term=30, premium_years=10,
                      arrow_path="arrow.png", coin_path="coin.png",
                      output_path="policy_timeline.png")

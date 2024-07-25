import os
import shutil
import customtkinter as ctk
from tkinter import messagebox
from PIL import Image as PilImage
import webbrowser
import sys

# Get the directory where the script is located
base_dir = os.path.dirname(os.path.abspath(__file__))

# Global variables for target_filename and minecraft_skins_folder
target_filename = ""
minecraft_skins_folder = ""
capename = ""

# Function to update the target_filename and path based on the selected cape
def select_cape(cape_name):
    global target_filename, minecraft_skins_folder, capename

    if cape_name == "15th Anniversary Cape":
        target_filename = "cd9d82ab17fd92022dbd4a86cde4c382a7540e117fae7b9a2853658505a80625"
        capename = "15th Anniversary Cape"
        minecraft_skins_folder = os.path.join(os.environ['APPDATA'], ".minecraft", "assets", "skins", "cd")

    elif cape_name == "Migrator Cape":
        target_filename = "2340c0e03dd24a11b15a8b33c2a7e9e32abb2051b2481d0ba7defd635ca7a933"
        capename = "Migrator's Cape"
        minecraft_skins_folder = os.path.join(os.environ['APPDATA'], ".minecraft", "assets", "skins", "23")

    elif cape_name == "Follower's Cape":
        target_filename = "569b7f2a1d00d26f30efe3f9ab9ac817b1e6d35f4f3cfb0324ef2d328223d350"
        capename = "Follower's Cape"
        minecraft_skins_folder = os.path.join(os.environ['APPDATA'], ".minecraft", "assets", "skins", "followers")

    elif cape_name == "Twitch Cape":
        target_filename = "cb40a92e32b57fd732a00fc325e7afb00a7ca74936ad50d8e860152e482cfbde"
        capename = "Twitch Cape"
        minecraft_skins_folder = os.path.join(os.environ['APPDATA'], ".minecraft", "assets", "skins", "cb")

    elif cape_name == "Vanilla Cape":
        target_filename = "f9a76537647989f9a0b6d001e320dac591c359e9e61a31f4ce11c88f207f0ad4"
        capename = "Vanilla Cape"
        minecraft_skins_folder = os.path.join(os.environ['APPDATA'], ".minecraft", "assets", "skins", "f9")

    elif cape_name == "Cherry Blossom Cape":
        target_filename = "afd553b39358a24edfe3b8a9a939fa5fa4faa4d9a9c3d6af8eafb377fa05c2bb"
        capename = "Cherry Blossom Cape"
        minecraft_skins_folder = os.path.join(os.environ['APPDATA'], ".minecraft", "assets", "skins", "af")
        
    else:
        messagebox.showerror("Error", "Invalid cape selection.")
        return
    show_main_page()

# Function to show the main page
def show_main_page():
    # Destroy the initial page and show the main cape selection interface
    for widget in app.winfo_children():
        widget.destroy()

    # Define paths
    assets_folder = os.path.join(base_dir, "All Minecraft Capes")

    # Define the capes file names
    capes = {
        "2011": "2011_cape.png",
        "2012": "2012_cape.png",
        "2013": "2013_cape.png",
        "2015": "2015_cape.png",
        "2016": "2016_cape.png",
        "Anniversary": "15Year_texture_JE.png",
        "TikTok": "TikTok_texture_BE.png",
        "Twitch": "Twitch_texture.png",
        "Cobalt": "Cobalt_Cape.png",
        "DannyBstyles": "DannyBstyles28texture_29.png",
        "Mapmaker": "MapmakerCapeTexture.png",
        "Millionth Customer": "Millionth_Customer_Cape_29.png",
        "MINECON 2019": "MINECON_2019_Cape_29.png",
        "Mojang": "Mojang_Cape_29.png",
        "Mojang Classic": "Mojang_Classic_cape_29.png",
        "Mojang Studios": "Mojang_Studios_Cape_29.png",
        "Party": "PartyCape.png",
        "Scrolls": "Scrolls_Cape.png",
        "Turtle": "Turtle_Cape_29.png",
        "Valentine": "Valentine_Cape_texture.png",
        "Vanilla": "Vanilla_Cape_Texture.png",
        "Cheapsh0t": "Cheapsh0t28texture29.png",
        "Unused Cape 1": "Unused_Cape_1.png",
        "Chinese Translator": "ChineseTranslatorCape.png",
        "Crowdin Translator": "CrowdinTranslatorCape.png",
        "MS Cape C": "MSCapeC.png",
        "Veterinarian": "Veterinarian_Cape.png",
        "Unused Cape 3T": "Unusedcape_3T.png",
        "Unused BE Cape 2": "UnusedBECape_2.png",
        "Unused BE Cape 1": "UnusedBECape_1.png",
        "Unused Cape 3": "Unused_Cape_3.png",
        "Microsoft Xbox 360": "MicrosoftXbox360_CapeT.png",
        "MrMessian": "MrMessiah28texture29.png",
        "Christmas 2010": "Christmas_2010_Cape_29.png",
        "Julian Clark": "JulianClark28texture29.png",
        "Bug Tracker": "BugTracker_Cape.png",
        "Progress Pride": "ProgressPrideCape_Texture_rv3.png",
        "Prismarine": "Prismarine_cape_29.png",
        "Pancape": "Pancape_Cape.png",
        "No Circle": "No_circle_Cape.png",
        "Bacon": "Bacon_Cape_29.png",
        "Awesome": "Awesom_Cape.png",
        "Nyan": "Nyan_Cape.png",
        "Xbox 1st Birthday": "Xbox_1st_Birthday_Cape_29.png",
        "New Years 2011": "New_Years_2011_Cape_29.png",
        "Blonk": "Blonk_Cape.png",
        "Bedwars": "Bedwars.png",
        "Heart": "Heart.png",
        "Youtube": "Sub2DelexoOnYoutube.png"
    }

    def change_cape(cape_file):
        source = os.path.join(assets_folder, cape_file)
        destination = os.path.join(minecraft_skins_folder, target_filename)
        try:
            shutil.copy(source, destination)
            messagebox.showinfo("Success!", f"Your {capename} now has altered into {cape_file}")
        except Exception as e:
            messagebox.showerror("Error", str(e))

    def open_donation_link(event):
        webbrowser.open_new("https://linktr.ee/delexo")

    def exit_program():
        app.destroy()

    # Create a frame for scrolling
    scrollable_frame = ctk.CTkScrollableFrame(master=app)
    scrollable_frame.pack(pady=20, padx=20, fill="both", expand=True)

    # Create a donation button and make it clickable
    donation_button = ctk.CTkButton(master=app, text="Buy me Coffee!", text_color="black", command=lambda: webbrowser.open_new("https://linktr.ee/delexo"), corner_radius=10, width=120, height=30, fg_color="white")
    donation_button.place(x=10, y=app.winfo_height()-50)

    # Create an exit button
    exit_button = ctk.CTkButton(master=app, text="Exit", text_color="white", command=exit_program, corner_radius=10, width=60, height=30, fg_color="red")
    exit_button.place(x=app.winfo_width()-70, y=10)

    # Load images and add buttons
    row = 1  # Start from the next row after the donation button
    col = 0
    for cape_name, cape_file in capes.items():
        if col == 3:  # Adjust the number of columns as needed
            col = 0
            row += 1

        image_path = os.path.join(assets_folder, cape_file)
        if not os.path.exists(image_path):
            print(f"Image not found: {image_path}")
            continue

        image = PilImage.open(image_path)
        image = image.resize((15, 15), PilImage.LANCZOS)  # Increase the image size
        photo = ctk.CTkImage(image)

        frame_inner = ctk.CTkFrame(master=scrollable_frame)
        frame_inner.grid(row=row, column=col, padx=10, pady=10)

        label = ctk.CTkLabel(master=frame_inner, text=cape_name, font=("Helvetica", 14))  # Update font size
        label.pack()

        button = ctk.CTkButton(master=frame_inner, image=photo, width=175, height=75, command=lambda cape_file=cape_file: change_cape(cape_file))  # Adjust button size
        button.image = photo  # Keep a reference to avoid garbage collection
        button.pack()

        col += 1

# Initialize the app
app = ctk.CTk()
app.title("Capes++ Client")
app.geometry("700x700")
app.resizable(False, False)  # Disable resizing

# Set appearance mode and color theme
ctk.set_appearance_mode("dark")  # Modes: "System" (default), "Dark", "Light"
ctk.set_default_color_theme("blue")  # Themes: "blue" (default), "green", "dark-blue"

# Create initial page
welcome_label = ctk.CTkLabel(app, text="Welcome to Capes++", font=("Helvetica", 40))  # Updated font size
welcome_label.pack(pady=10)

choose_label = ctk.CTkLabel(app, text="Which one of these Capes do you currently have equipped?", font=("Helvetica", 14))  # Updated font size
choose_label.pack(pady=10)

anniversary_button = ctk.CTkButton(app, text="15th Anniversary Cape", command=lambda: select_cape("15th Anniversary Cape"), width=300, height=60)
anniversary_button.pack(pady=10)

migrator_button = ctk.CTkButton(app, text="Migrator Cape", command=lambda: select_cape("Migrator Cape"), width=300, height=60)
migrator_button.pack(pady=10)

followers_button = ctk.CTkButton(app, text="Follower's Cape", command=lambda: select_cape("Follower's Cape"), width=300, height=60)
followers_button.pack(pady=10)

twitch_button = ctk.CTkButton(app, text="Twitch Cape", command=lambda: select_cape("Twitch Cape"), width=300, height=60)
twitch_button.pack(pady=10)

vanilla_button = ctk.CTkButton(app, text="Vanilla Cape", command=lambda: select_cape("Vanilla Cape"), width=300, height=60)
vanilla_button.pack(pady=10)

cherry_blossom_button = ctk.CTkButton(app, text="Cherry Blossom Cape", command=lambda: select_cape("Cherry Blossom Cape"), width=300, height=60)
cherry_blossom_button.pack(pady=10)

# Run the application
app.mainloop()

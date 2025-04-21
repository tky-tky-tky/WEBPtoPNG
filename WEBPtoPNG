import os
import tkinter as tk
import shutil
from tkinter import filedialog
from PIL import Image

def convert_webp_to_png(input_folder, output_folder):
    os.makedirs(output_folder, exist_ok=True)

    for folder in input_folder:
        for filename in os.listdir(folder):
            file_path = os.path.join(folder, filename)

            if filename.lower().endswith(".webp"):
                png_path = os.path.join(output_folder, os.path.splitext(filename)[0] + ".png")

                # WebP → PNG に変換
                img = Image.open(file_path).convert("RGB")
                img.save(png_path, "PNG")

                # 元のWebPファイルを削除
                os.remove(file_path)

            else:
                # WebP以外はそのまま移動
                output_path = os.path.join(output_folder, filename)
                shutil.move(file_path, output_path)
        
        # フォルダが空になったら削除
        if not os.listdir(folder):
            os.rmdir(folder)
            print(f"空のフォルダを削除しました: {folder}")


def process_selected_folders(parent_folder):
    #アプリと同じ位置にフォルダを生成し出力します。任意のフォルダ名に変更してください
    base_output_folder = os.path.join(os.path.dirname(__file__), "_出力用")
    os.makedirs(base_output_folder, exist_ok=True) #該当フォルダなければ作成

    for foldername in os.listdir(parent_folder):
        folder_path = os.path.join(parent_folder, foldername) #子フォルダのパスを作成
        if os.path.isdir(folder_path): #フォルダであるなら
            new_folder_name = foldername
            new_folder_path = os.path.join(base_output_folder, new_folder_name) #出力先のパスを作成


            #重複するフォルダ名に連番を付ける
            counter = 1
            while os.path.exists(new_folder_path):
                new_folder_name = f"{foldername} ({counter})"
                new_folder_path = os.path.join(base_output_folder, new_folder_name)
                counter += 1

            os.makedirs(new_folder_path, exist_ok=True)

            convert_webp_to_png([folder_path], new_folder_path)
            print(f"Conversion complete. images saved in {new_folder_path}")

def main():
    root = tk.Tk()
    root.withdraw()  # メインウィンドウを非表示にする

    selected_folder = filedialog.askdirectory(title="親フォルダを選択してください")
    if selected_folder:
        process_selected_folders(selected_folder)
        print("すべての処理が完了しました。")

if __name__ == "__main__":
    main()

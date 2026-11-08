# Skill-editing-
/skills 

import requests 

def hyperframes_edit(input_file, output_file, operations):
    payload = {
        "input": input_file,
        "output": output_file,
        "operations": operations
    }
    response = requests.post(
        "http://localhost:8000/api/v1/edit",
        json=payload,
        timeout=300
    )
    response.raise_for_status()
    return response.json()

result = hyperframes_edit(
    input_file="clip.mp4",
    output_file="final_edit.mp4",
    operations=[
        {"type": "trim", "start": 5, "end": 25},
        {"type": "filter", "name": "cinematic"},
        {"type": "subtitle", "text": "Intro", "position": "bottom"},
        {"type": "audio", "normalize": True}
    ]
) import subprocess

def ffmpeg_edit(input_file, output_file, filters):
    cmd = [
        "ffmpeg",
        "-i", input_file,
        "-vf", filters,
        "-y", output_file
    ]
    subprocess.run(cmd, check=True)

"scale=1920:1080:force_original_aspect_ratio=decrease,eq=contrast=1.1:saturation=1.3"

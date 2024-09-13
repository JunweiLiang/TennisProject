# note on using tennis tools

### tennis-tracking

+ Usage
    ```
    # https://github.com/JunweiLiang/tennis-tracking/
    # 26 second video takes 1.5 hr to process on rtx 2060 laptop

        # ball tracking is bad, but can capture court lines and has a minimap visualization
        # camera view suggestion: full court in sight, 4 meter up, wide len is fine
            # see IMG_1771_wide_lower.mov: https://drive.google.com/file/d/1MrLEgbZ1C6gGUS_DK87gir8yUfJUbEA5/view?usp=sharing


        # example command:
            (tennis) junweil@precognition-laptop2:~/projects/tennis/tennis-tracking$ python predict_video.py --input_video_path=../rally_top_down_view_for_analysis/IMG_1783_wide_serve.mp4 --output_video_path=../rally_top_down_view_for_analysis/tennis-tracking/IMG_1783_wide_serve.mp4 --output_video_with_minimap_path=../rally_top_down_view_for_analysis/tennis-tracking/IMG_1783_wide_serve_with_minimap.mp4 --minimap=1 --bounce=1

        # 效果：球场线识别可以，球追踪差，20秒视频要1.5小时处理，RTX 2060

    ```

### tennis_analysis

+ Usage
    ```
    # https://github.com/abdullahtarek/tennis_analysis
    # modified the code to take input output arguments

        # 09/12/2024: not able to run, this does not account for bad player tracking

        (base) junweil@precognition-laptop2:~/projects/tennis/tennis_analysis$ python main.py ../rally_top_down_view_for_analysis/IMG_1778_zoom1.0.mp4 ../rally_top_down_view_for_analysis/tennis_analysis/IMG_1778_zoom1.0.mp4


    ```

### TennisProject
+ install
    ```
    $ conda create -n TennisProject python=3.7
    $ pip install numpy==1.19.3
    $ pip install scipy==1.3.1
    (TennisProject) junweil@precognition-laptop2:~/projects/tennis/TennisProject$ pip install -r requirements.txt

    # download the fpn model
        $ wget https://download.pytorch.org/models/fasterrcnn_resnet50_fpn_coco-258fb6c6.pth

        (TennisProject) junweil@precognition-laptop2:~/projects/tennis/TennisProject$ mv ../fasterrcnn_resnet50_fpn_coco-258fb6c6.pth /home/junweil/.cache/torch/checkpoints/fasterrcnn_resnet50_fpn_coco-258fb6c6.pth

    ```
+ Usage
    ```
    # https://github.com/yastrebksv/TennisProject
        # https://github.com/JunweiLiang/TennisProject

    # download the models into models/

    # need to prepare videos in 1280x720

        (TennisProject) junweil@precognition-laptop2:~/projects/tennis/TennisProject$ python main.py --path_ball_track models/model_best_tracknet.pt --path_court models/model_tennis_court_det.pt --path_bounce_model models/ctb_regr_bounce.cbm --path_input ../rally_top_down_view_for_analysis/IMG_1771_wide_lower_crop_720p.mp4 --path_output ../rally_top_down_view_for_analysis/TennisProject/IMG_1771_wide_lower_crop_720p.mp4

        # RTX 2060 20秒视频10分钟处理完，速度很快
        # 效果： 球场线识别噪音大，ball tracking and ball bounce detection is good

    ```

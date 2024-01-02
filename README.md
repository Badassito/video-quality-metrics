FORK NOTES : I have no idea what I'm doing, please refer to whatever the source of a fork is called

1. Added SVT-AV1 and presets
# Video Quality Metrics (VQM)

You can check the available arguments with `python main.py -h`:

```
usage: main.py [-h] [--av1-cpu-used <1-8>] [-cl <1-60>] [-crf <0-51> [<0-51> ...]] [-dp DECIMAL_PLACES] [-e {x264,x265,libaom-av1}] [-i <1-600>] [-subsample SUBSAMPLE]
               [--n-threads N_THREADS] [-ntm] [-o OUTPUT_FOLDER] -ovp ORIGINAL_VIDEO_PATH [-p <preset/s> [<preset/s> ...]] [--phone-model] [-sc] [-psnr] [-ssim] [-msssim]
               [-t SECONDS] [-tvp TRANSCODED_VIDEO_PATH] [-vf VIDEO_FILTERS]

optional arguments:
  -h, --help            show this help message and exit

Encoding Arguments:
  --av1-cpu-used <1-8>  Only applicable if the libaom-av1 (AV1) encoder is chosen. Set the quality/encoding speed tradeoff. Lower values mean slower encoding but better
                        quality, and vice-versa (default: 5)
  -crf <0-51> [<0-51> ...]
                        Specify the CRF value(s) to use
  -e {x264,x265,libaom-av1}, --video-encoder {x264,x265,libaom-av1}
                        Specify whether to use the x264 (H.264), x265 (H.265) or libaom-av1 (AV1) encoder (default: x264)
  -p <preset/s> [<preset/s> ...], --preset <preset/s> [<preset/s> ...]
                        Specify the preset(s) to use (default: medium)

VMAF Arguments:
  -subsample SUBSAMPLE  Set a value for libvmaf's n_subsample option if you only want the VMAF/SSIM/PSNR to be calculated for every nth frame. Without this argument,
                        VMAF/SSIM/PSNR scores will be calculated for every frame (default: 1)
  --n-threads N_THREADS
                        Specify the number of threads to use when calculating VMAF
  --phone-model         Enable VMAF phone model (default: False)

Overview Mode Arguments:
  -cl <1-60>, --clip-length <1-60>
                        When using Overview Mode, a X seconds long segment is taken from the original video every --interval seconds and these segments are concatenated to
                        create the overview video. Specify a value for X (in the range 1-60) (default: 1)
  -i <1-600>, --interval <1-600>
                        To activate Overview Mode, this argument must be specified. Overview Mode creates a lossless overview video by grabbing a --clip-length long segment
                        every X seconds from the original video. Specify a value for X (in the range 1-600) (default: None)

General Arguments:
  -dp DECIMAL_PLACES, --decimal-places DECIMAL_PLACES
                        The number of decimal places to use for the data in the table (default: 2)
  -ntm, --no-transcoding-mode
                        Enable "no transcoding mode", which allows you to calculate the VMAF/SSIM/PSNR for a video that you have already transcoded. The original and
                        transcoded video paths must be specified using the -ovp and -tvp arguments, respectively. Example: python main.py -ntm -ovp original.mp4 -tvp
                        transcoded.mp4 (default: False)
  -o OUTPUT_FOLDER, --output-folder OUTPUT_FOLDER
                        Use this argument if you want a specific name for the output folder. If you want the name of the output folder to contain a space, the string must
                        be surrounded in double quotes (default: None)
  -ovp ORIGINAL_VIDEO_PATH, --original-video-path ORIGINAL_VIDEO_PATH
                        Enter the path of the original video. A relative or absolute path can be specified. If the path contains a space, it must be surrounded in double
                        quotes (default: None)
  -sc, --show-commands  Show the FFmpeg commands that are being run. (default: False)
  -t SECONDS, --encode-length SECONDS
                        Create a lossless version of the original video that is just the first x seconds of the video. This cut version of the original video is what will
                        be transcoded and used as the reference video. You cannot use this option in conjunction with the -i or -cl arguments (default: None)
  -tvp TRANSCODED_VIDEO_PATH, --transcoded-video-path TRANSCODED_VIDEO_PATH
                        The path of the transcoded video (only applicable when using the -ntm mode) (default: None)
  -vf VIDEO_FILTERS, --video-filters VIDEO_FILTERS
                        Add FFmpeg video filter(s). Each filter must be separated by a comma. Example: -vf bwdif=mode=0,crop=1920:800:0:140 (default: None)

Optional Metrics:
  -psnr, --calculate-psnr
                        Enable PSNR calculation in addition to VMAF (default: False)
  -ssim, --calculate-ssim
                        Enable SSIM calculation in addition to VMAF (default: False)
  -msssim, --calculate-msssim
                        Enable MS-SSIM calculation in addition to VMAF (default: False)
```

# Requirements

1. Python **3.6+**
2. `pip install -r requirements.txt`
3. FFmpeg and FFprobe installed and in your PATH (or in the same directory as this program). Your build of FFmpeg must have v2.1.1 (or above) of the libvmaf filter. Depending on the encoder(s) that you wish to test, FFmpeg must also be built with libx264, libx265 and libaom.

# pi5_whisper_voice_assistant
This is a Raspberry Pi 5 whisper C++ voice assistant - backwards compatible with Pi4
See the video of how it works here:

1. git clone https://github.com/ggerganov/whisper.cpp
2. Install libraries:
3. sudo apt-get install libgpiod2 libgpiod-dev
4. sudo apt install gpiod
5. sudo apt install libsdl2-dev

cd whisper.cpp

In the whisper.cpp directory open up the Makefile and add "-lgpiod" to the end of the line starting with CC_SDL and save the Makefile. This links the newly installed gpiod library. Otherwise you'll get a linking error.  
CC_SDL=`sdl2-config --cflags --libs` -lgpiod

Download the model(s) that you'd like to use. Raspberry pi 4 only works well with tiny.en. Raspberry pi 5 works well up to small.en
./models/download-ggml-model.sh tiny.en
./models/download-ggml-model.sh base.en
./models/download-ggml-model.sh small.en

compile the stream program
make -j stream

Run it in your terminal (pi 4 should stick with tiny.en.bin, pi 5 can go up to the small.en.bin model)
./stream -m models/ggml-tiny.en.bin --step 4000 --length 8000 -c 0 -t 4 -ac 512

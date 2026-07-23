# Speech Decryption
Here we would be doing the same thing, i.e de cryption but on the audio. so take any audio dataset you wish. I used a dataset from this site- https://www.openslr.org/12 known as dev-clean. Just download the zipped folder and modify the path to the dataset while running locally accordingly.

How do we get data from audio?, Well we use fourier transforms!. what is that- in simple terms it gives us the magnitudes of different freq. sine waves which consititue the audio. So the data you get is the fourier tranform of the audio. We generally do the real time fourier transform.       
--Why real?(Just for info)---               
We generally do the real time fourier transform since all our audio signal are real. Because of this we can show that the magnitudes of negative freq. are conjugates of the positive freq. and resultant is real number.     

# Pre-processing
1. Download and import the dataset
2. Include these libraries
```
import librosa       # to open/load the audio files
import scipy.fft as fft    # to generate fft data
import soundfile as sf`  # to generate audio files
```
3 . Finding the freq positions for fft
````
target_sr = 17000      # sampling rate generally for all human voices max freq is 17k around
chunk_size = 25000      # generally the audio is long so divided into some chuncks, each of size 25000
# doing fft results in N/2+1 points
base_frequencies = fft.rfftfreq(chunk_size, 1/target_sr)[:-1]  # finding the frequency points,and take (12500 now)
rfft_size = len(base_frequencies) 

````
4 . Making the dataset:
````
  all_magnitudes = []
  all_frequencies = []
  for video_path in audio_paths:        # for all audio
    y, sr = librosa.load(video_path, sr=target_sr)    # load the fourier data
    N = len(y)
    
    # Chop into fixed chunks (only if your size of video is long >7-8 ms)
    audio_parts = np.array([y[x:x+chunk_size] for x in range(0, N, chunk_size) if x+chunk_size <= N])
    if len(audio_parts) == 0:    # remove those with size 0
        continue  
    fourier_transforms = np.array([fft.rfft(part) for part in audio_parts])
    
    # Extract magnitude and drop the last bin to match frequencies (12500)
    fourier_mag = np.abs(fourier_transforms)[:, :-1]    # again remove that last one
    fourier_mag = fourier_magnitudes.astype(np.float32)
    all_magnitudes.append(fourier_magnitudes)
    all_frequencies.append(np.tile(base_frequencies, len(audio_parts)).astype(np.float32))
  total_magnitudes = np.concatenate(all_magnitudes)
  total_frequencies = np.concatenate(all_frequencies).reshape(-1, rfft_size)
````
total_magnitudes and total_frequencies are the data here
NOTE: This is just an example you can change parameters here.  We would keep phase same and apply cipher to the magnitude. to extract phase use np.angle()

# Encryption
1.take the total_magnitudes apply cipher to it- ceiser/permuation or any key cipher         
2. Make the dataset with actual and cipherd and the key/permuation used

# Model
You can use either transformer or GAN fo for this, GAN is little bit hard to train so if you try gan try cracking easier cipher.
NOTE: if you do not use GAN in final project, ensure you remove Adversarial networks when you mention this project in your resume later, since GANs are only considered adversarial

# reconstruction of sound
use this block to reconstruct the sound back- pass on the magnitudes and the original fft done in the beginning, since you didnt alter the phase we need that phase to reconstruct it back.
````
def reconstruct_with_phase(mags, original_complex_fft):
    true_phase = np.angle(original_complex_fft)
    padded_mags = np.pad(mags, ((0,0), (0,1)), mode='constant')
    rebuilt_complex = padded_mags * np.exp(1j * true_phase)
    waves = fft.irfft(rebuilt_complex, axis=1)
    return waves.flatten()
````

# Final tips for GAN
1. If the generator loss is  getting larger, just reduce the lr of the discriminator. generally works
2. dont include higher complex ciphers, keep it simple thats the reason why i kept phase the same, if you try applying cipher to phase, it becomes quite messy and gan cannot learn it easily.

You can see an example gan model here: A image deblur gan model:         
https://resilient-bobcat-453.notion.site/Image-Deblurring-using-Deep-Learning-2c32ccbc5b848017b5f4ffb2cab04a10 


   
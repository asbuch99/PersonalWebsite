---
Title: Air Gapped Raspberry Pi based Linux log in
menu: "main"
---


# Facial Recognition Project

This project is aimed at developing a air gapped facial recognition system using  Python and other various libraries.  

It can be found at: [Github for Air Gapped Facial Recognition](https://github.com/asbuch99/FacialRecogProj/)  
A downloadable report for this project can be found here: [Report](https://github.com/asbuch99/FacialRecogProj/blob/main/Project%20Report.pdf)

## Objectives:

1. Implementing a facial detection algorithm.
2. Training a model to recognize faces.
3. Integrating the trained model into a real-time application.
4. Deploying the application to various platforms.
5. Do all this while ensuring the log in module is secure by keeping it air gapped

## Project Structure:

The project is organized as follows:

- **src/**: Contains the source code for the facial recognition system.
  - `facial_detection.py`: Script for detecting faces in images or video streams.
  - `facial_recognition.py`: Script for training and recognizing faces.
  - `app.py`: Main application script for real-time face recognition.
- **data/**: Contains datasets for training the facial recognition model.
  - `faces/`: Directory containing labeled face images for training.
- **models/**: Saved models after training.
- **docs/**: Documentation files.
- **requirements.txt**: Dependencies required to run the project.
- **etcprof.sh**: Login script modified to bypass the main Linux login screen and default to the Raspberry Pi.

### Explanation of etcprof.sh snippet:

The provided snippet is a part of the `etcprof.sh` script, and it performs the following  
actions:

```bash
if [ "`id -u -n`" == "anvay" ]; then
    ssh -tt tacwin@rpi4.local 2> /dev/null | grep -i "anvay" > /dev/null 
    if [ "$?" -ne "0" ]; then
        now=`date +"%D   %T"`
        echo "login failed at $now" >> /var/attempt_log.log
        exit 1
    else
        now=`date +"%D   %T"`
        echo "login successful at $now" >> /var/attempt_log.log
    fi
fi
```


- The if statement checks if the current user executing the script is "anvay". It uses the id -u -n command to get the current username.

- If the user is "anvay", it proceeds with the subsequent commands.

- Inside the if block, it attempts to SSH into the tacwin account on the host rpi4.local.

- The 2> /dev/null redirects the standard error output to /dev/null to suppress any error messages.

- The output of the SSH command is piped to grep -i "anvay" to search for occurrences of the username "anvay" in the SSH output.

- The > /dev/null at the end of the pipeline redirects the output of grep to /dev/null to discard it.

- The if [ "$?" -ne "0" ] condition checks if the exit status of the previous command (grep) is not equal to 0, indicating a failure.

- If the SSH command fails to find "anvay" in the output, it logs a "login failed" message along with the timestamp to /var/attempt_log.log file.

- If the SSH command is successful, it logs a "login successful" message along with the timestamp to the same log file.

- The exit 1 statement terminates the script with an exit code of 1, indicating a failure.






## Usage:

1. Clone the repository:
    ```
    git clone https://github.com/asbuch99/FacialRecogProj.git
    ```

2. Install dependencies:
    ```
    pip install -r requirements.txt
    ```

3. Train the model:
    ```
    python src/facial_recognition.py --train
    ```

4. Run the real-time face recognition application:
    ```
    python src/app.py
    ```

## Contributions:

Contributions to this project are welcome! If you'd like to contribute, please follow these steps:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Make your changes.
4. Commit your changes (`git commit -am 'Add some feature'`).
5. Push to the branch (`git push origin feature/your-feature`).
6. Create a new Pull Request.

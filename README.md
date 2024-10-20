# Docker_ESP-IDF
Setting up ESP-IDF using Docker [On Windows]
# Software requirements
1. Docker: Install Docker for Windows from https://docs.docker.com/desktop/install/windows-install/ and set it up according to the instructions.
   
2. ESP - IDF: Install and setup ESP-IDF from https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/windows-setup.html
  
3. ESP RFC2217 Server: Download, extract and install esptool from https://github.com/espressif/esptool/releases
   

# Hardware requirements
1. ESP32 Dev board

2. Micro USB Cable

# Steps
1. Open ESP-IDF CMD and Docker application
   
2. Create a Project Directory: In the ESP - IDF CMD, create a new directory for your ESP32 project. This will be your working directory. Use the command
   
mkdir <project_directory>

4. Navigate to Your Project Directory: Change to your project directory. Use the command
   
cd <project_directory>

6. Pull the ESP-IDF Docker Image: If you haven't pulled the ESP-IDF Docker image previously, run the following command:
   
docker pull espressif/idf

8. Run the Docker Container: Start the Docker container, mounting your project directory to the /project directory inside the container.
   
docker run --rm -v <path_to_your_project_directory>:/project -w /project -e HOME=/tmp -it espressif/idf

10. Clean and Build the Project: Inside the Docker container, clean the previous build (if any) and build the project using the following commands:
    
idf.py fullclean

idf.py build

12. Set Up the RFC2217 Server: On your host machine, open the command prompt and navigate to where esp_rfc2217_server is located. Start the server with the desired COM port.
    
esp_rfc2217_server -v -p <port_number> <COM_port>

Replace <port_number> with the desired port (e.g., 4000) and <COM_port> with your actual COM port (e.g., COM3, COM7, etc.).

14. Flash the Built Project: In the Docker container, run the following command to flash the built project to your ESP32 device:
    
idf.py -p 'rfc2217://host.docker.internal:<port_number>?ign_set_control' flash

Replace <port_number> with the port you specified when starting the RFC2217 server.

16. Monitor Output (Optional): You can monitor the output while flashing by running:
    
idf.py -p 'rfc2217://host.docker.internal:<port_number>?ign_set_control' flash monitor

# References
1. https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/windows-setup.html

2. https://docs.docker.com/desktop/install/windows-install/

3. https://github.com/espressif/esptool/releases

4. https://github.com/espressif/vscode-esp-idf-extension/blob/master/docs/tutorial/install.md

5. https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-guides/tools/idf-docker-image.html

6. https://github.com/espressif/vscode-esp-idf-extension/blob/master/docs/tutorial/using-docker-container.md

7. https://www.hackster.io/leoribg/esp-idf-in-docker-dev-container-e8510f



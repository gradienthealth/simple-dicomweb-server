# simple-dicomweb-server

This is a simple docker-compose app to run an Orthanc dicom server. Orthanc is meant to emulate a production dicom PACS which supports dicomweb.

### Getting Started

1. Download [docker](https://www.docker.com/) for your operating system.

2. Install [docker-compose](https://docs.docker.com/compose/install/) for your operating system.

3. Git clone this repo with `git clone https://github.com/gradienthealth/simple-dicomweb-server.git`

4. Change into the root of this repo and run `docker-compose up`

5. Navigate to `http://localhost:3337/app/explorer.html#upload` and upload your dicom data via the Orthanc UI.

<img width="891" alt="image" src="https://user-images.githubusercontent.com/5455421/187281349-03c4fd45-5f23-4d26-86a8-649af239644a.png">

6. Get the StudyUUID metadata from all the studies with the following linux command line. This will produce a file called `studies.csv` in the directory the command is run.
```bash
docker run -i --network host --rm curlimages/curl -k http://localhost:3337/tools/find \
    -d '{"Level" : "Study", "Expand":true, "Query":{"PatientID" : "*"}}' |
docker run --rm -i imega/jq \
    -r '.[].MainDicomTags.StudyInstanceUID' > studies.csv
```

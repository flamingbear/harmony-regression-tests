# Generates a pre-computed (solved) set of dependencies from the
# environment.yaml file. This should be updated if the
# environment.yaml has changed, and the resulting file
# (environment-linux-64.conda.lock) should be committed.
harmony-image-lockfile: harmony/environment.yaml
	docker run -i --volume "${PWD}:/harmony-rt" -t continuumio/miniconda3:4.9.2 bash -c "conda install -y -c conda-forge conda-lock; cd /harmony-rt/harmony; conda-lock -f environment.yaml -p linux-64 --filename-template \"environment-{platform}.conda.lock\"; ls -al"

harmony-image: Dockerfile harmony/environment.yaml
	docker build -t harmony/regression-tests-harmony:latest -f ./Dockerfile --build-arg notebook=Harmony.ipynb --build-arg sub_dir=harmony .

asf-gdal-image: Dockerfile gdal_subsetter/environment.yaml
	docker build --no-cache -t harmony/regression-tests-asf-gdal:latest -f ./Dockerfile --build-arg notebook=GDAL_Subsetter_Regression.ipynb --build-arg sub_dir=gdal_subsetter .

harmony-regression-image: Dockerfile harmony-regression/environment.yaml
	docker build --no-cache -t harmony/regression-tests-harmony-regression:latest -f ./Dockerfile --build-arg notebook=HarmonyRegression.ipynb --build-arg sub_dir=harmony-regression .

images: harmony-image asf-gdal-image harmony-regression-image

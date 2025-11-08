FROM public.ecr.aws/lambda/python:3.13

# install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# work in Lambda task root
WORKDIR ${LAMBDA_TASK_ROOT}

# copy dependency manifest first (better cache)
COPY pyproject.toml ./

# install deps into a local venv under /var/task/.venv
RUN uv sync --no-dev --python 3.13

# copy your handler last
COPY handler.py ./handler.py

# make sure Python can find the venv’s site-packages
ENV PYTHONPATH="${LAMBDA_TASK_ROOT}/.venv/lib/python3.13/site-packages"

# set the Lambda entrypoint: <module>.<function>
CMD ["handler.exif_handler"]

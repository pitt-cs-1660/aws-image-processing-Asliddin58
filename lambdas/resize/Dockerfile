FROM public.ecr.aws/lambda/python:3.13

# install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# work in Lambda task root
WORKDIR ${LAMBDA_TASK_ROOT}

# copy dependency manifest
COPY pyproject.toml ./

# install deps into a local venv 
RUN uv sync --no-dev --python 3.13

# copy handler last
COPY handler.py ./handler.py

# venv site-packages
ENV PYTHONPATH="${LAMBDA_TASK_ROOT}/.venv/lib/python3.13/site-packages"

# set the Lambda entrypoint
CMD ["handler.resize_handler"]

FROM oven/bun as builder
WORKDIR /usr/src/app
COPY package.json bun.lockb tsconfig.json ./
RUN bun install
RUN bun build:frontend

FROM oven/bun as tester
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app /usr/src/app
COPY ./frontend ./frontend

FROM oven/bun as dev
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app /usr/src/app
COPY ./frontend ./frontend
RUN bun start:frontend

FROM node as prod
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app/build/frontend /usr/src/app/
ENTRYPOINT [ "node", "index.js" ]

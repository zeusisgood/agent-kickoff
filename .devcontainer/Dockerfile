# ベースは言語の公式 slim イメージ（例: golang:1-trixie, rust:slim-trixie, python:3-slim-trixie）。
# なければ debian:trixie-slim。devcontainer.json の BASE_IMAGE で切り替える。
ARG BASE_IMAGE=debian:trixie-slim
FROM ${BASE_IMAGE}

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000
# エージェントの CLI を入れるか。使わないエージェントは false にする（他のエージェントは、この下に同じ形で足す）
ARG INSTALL_CLAUDE_CODE=true

# 共通の道具。言語の道具は案件ごとにこの RUN に足す（RUN を増やさない）。
# sudo は入れない（Claude に root を渡さない）。足したい道具は Dockerfile に書いて作り直す。
# UID・GID が使用中（node の node、ubuntu の ubuntu など）なら、その持ち主を消してから作る。
# 別の UID で作ると、Dev Containers が手元の UID に合わせられず、ワークスペースに書き込めない。
# それでも作れない（GID が別の利用者の主グループ、など）ときは、別の番号に逃げずにビルドを失敗させる。
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
      ca-certificates curl git gh less jq ripgrep openssh-client \
 && rm -rf /var/lib/apt/lists/* \
 && if ! id -u "${USERNAME}" >/dev/null 2>&1; then \
      old=$(getent passwd "${USER_UID}" | cut -d: -f1) \
      && { [ -z "$old" ] || userdel -r "$old"; } \
      && old=$(getent group "${USER_GID}" | cut -d: -f1) \
      && { [ -z "$old" ] || groupdel "$old"; } \
      && groupadd --gid "${USER_GID}" "${USERNAME}" \
      && useradd --uid "${USER_UID}" --gid "${USER_GID}" -m -s /bin/bash "${USERNAME}"; \
    fi

USER ${USERNAME}
WORKDIR /home/${USERNAME}

# Claude Code はネイティブインストーラで入れる（Node.js 不要）。
# .claude は先に作っておき、名前付きボリュームの持ち主を vscode にする。
RUN mkdir -p /home/${USERNAME}/.claude \
 && if [ "${INSTALL_CLAUDE_CODE}" = "true" ]; then curl -fsSL https://claude.ai/install.sh | bash; fi

ENV PATH="/home/${USERNAME}/.local/bin:${PATH}"
